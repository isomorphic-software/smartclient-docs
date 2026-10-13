# Report Delivery and Scheduling

[← Back to API Index](../reference.md)

---

## KB Topic: Report Delivery and Scheduling

### Description
**Report Delivery: Share Now, schedules and rendering on the server**

A [ReportBuilder](../classes/ReportBuilder.md#class-reportbuilder) report can be emailed immediately (_Share Now_), emailed on a schedule, or produced as a file on the server. Three parts make this up, and they can be used together or separately:

1.  **Rendering a report to a file**: the server produces a published report as a PNG snapshot, an Excel workbook or a PDF.
2.  **The schedule contract**: the `rb_scheduled_reports` DataSource stores what to send, to whom and when, and `rb_report_delivery_runs` ("deliver now") sends a stored schedule on demand. Any scheduler can drive delivery through these two DataSources.
3.  **The built-in scheduler**: an optional, single-server demonstration that fires stored schedules from this server's Quartz instance. For production use, drive delivery from your organization's own scheduler instead.

**Enabling delivery**

Delivery is off until a deployment configures it, in `server.properties`:

*   `reportDelivery.enabled: true`, with outgoing mail configured through the standard `mail.system.*` settings; `reportDelivery.fromAddress` optionally sets the sender of report emails.
*   `reportRender.baseUrl`: the scheme, host and port by which this server reaches _itself_ to render a report. It must address this server instance, not a load balancer in front of several. Rendering also needs the WebDriver support jars and Chrome on the server: see _Installing the renderer_ below.
*   `reportScheduler.enabled: true` to store and deliver schedules, and additionally `reportScheduler.builtInTrigger: true` to have the built-in scheduler fire them.

Every setting is described in `framework.properties`.

**Installing the renderer**

Snapshots, Excel and PDF files of a report are produced by opening the report page in headless Chrome on the server, driven through Selenium WebDriver. Without them, Share Now and scheduled emails still send, without the snapshot or attachments.

*   **The WebDriver support jars.** An SDK includes them in `WEB-INF/lib`: `isomorphic_webdriver.jar` plus the Selenium jars and their dependencies, listed in the `installJars` script in `WEB-INF/lib-WebDriverSupport`. A deployment that trims `WEB-INF/lib` must keep those jars. With Maven, add the `isomorphic-webdriver` artifact (see [mavenSupport](mavenSupport.md#kb-topic-maven-support)), which brings in Selenium.
*   **Chrome.** Install Google Chrome or Chromium on the server; no display is needed. Selenium (Selenium Manager) finds an installed Chrome or Chromium and downloads the `chromedriver` matching its version, and downloads Chrome too if none is installed, which needs internet access from the server and a writable home directory for its cache. A chromedriver set JVM-wide (the `webdriver.chrome.driver` system property) or found on the PATH is not used, since it may not match. On a server without internet access, install both and set `reportRender.chromeBinary` and `reportRender.chromeDriver` to their executables; a chromedriver must match Chrome's major version.
*   **The server environment.** Each render starts its own Chrome for the length of the render (allow a few hundred MB per concurrent render), with the flags containers need (no sandbox, no shared-memory dependency). On Linux, install the usual fonts (for example DejaVu or Liberation) or text in snapshots may draw as boxes. `reportRender.timeoutSeconds` (default 90) bounds each render, and `reportRender.maxConcurrent` (default 3) how many run at once; see _Security_ below.

To check an installation, call `com.isomorphic.rpc.ReportRenderer.isAvailable()` (whether the support jars are present), then deliver a schedule once with "deliver now": the reason for any file that could not be produced is in its result and the schedule's `lastRunMessage`, and in the server log.

**Delivery outside Reify**

Delivery works in a standalone SmartClient application, one using the SmartClient server without Reify, just as it does in Reify. What such an application has to provide is a _report page_ for each report.

_Report pages_. A report's content exists only in a browser: its snapshot, the data behind each component and its print layout are produced by the live `DataReport`. So a report is identified by a _report page_, an ordinary page of the application (not a service endpoint) that shows the report when opened, and the server renders a report by opening that page in headless Chrome: at `reportRender.baseUrl` plus the page's site-relative path, which is what a schedule stores. Once the page is idle, the server asks the first drawn `DataReport` on it to render itself, and builds the files from what it sends back. A report page must therefore:

*   draw its report on load, with no user action, and draw no other report;
*   load the report's data as part of loading, so the report is complete once the page is idle;
*   have a stable address, since schedules keep it;
*   be open to the user the report is rendered as (see authentication, below).

`reportRender.reportPathPattern`, a regular expression over the page's path, lists the pages that are report pages. It is a security check: a schedule's address comes from a client and the server's browser may open it logged in as the schedule's owner, so any other page is refused rather than opened. The default accepts Reify's report page (`projectRunner.jsp`) and the SDK's.

_The SDK's report page_, `tools/reporting/reportPage.jsp`, shows one saved report by name: `reportPage.jsp?report=`_name_, with an optional `&skin=`. It loads the report with [RPCManager.loadScreen](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen): a report a [ReportBuilder](../classes/ReportBuilder.md#class-reportbuilder) saved (to its [ReportBuilder.screenDataSource](../classes/ReportBuilder.md#attr-reportbuilderscreendatasource)), or a `.ui.xml` file on the `project.ui` path, looked up for the logged-in user. A ReportBuilder with [ReportBuilder.reifyIntegration](../classes/ReportBuilder.md#attr-reportbuilderreifyintegration) `false` points schedules at it unless told otherwise, so reports built and saved there can be shared and scheduled with no further setup. It is also a template: copy it to give reports the application's own skin, modules or surroundings.

In short, a standalone application should:

*   use the SDK's report page, or its own, with `reportRender.reportPathPattern` set to match its path (for example `/app/reports/view\.jsp(\?.*)?`);
*   for its own page, tell reports their address where they are edited elsewhere: set [ReportBuilder.reportPageURL](../classes/ReportBuilder.md#attr-reportbuilderreportpageurl) (or [DataReport.reportPageURL](../classes/DataReport.md#attr-datareportreportpageurl) on a report shown outside a builder). On the report page itself the current page is used;
*   let the server's browser log in, for reports that show each user their own data (see _Logging in the server's browser_, below);
*   ignore sandboxes unless it uses sandboxed databases (see _Sandboxed databases_ below).

_Logging in the server's browser_. Sharing, scheduling and ownership follow the request's authenticated user, and a schedule renders as its owner. For that, the server opens the report page with a one-time login token in its query string ([LoginTokens](server/javadoc/com/isomorphic/auth/LoginTokens.html)): accepted once, within two minutes, on that page only, and only from the server's own machine. How the token is honoured depends on the application's authentication:

*   SmartClient's `AuthenticationFilter` in front of the report page honours it with no further work;
*   an application's own authentication honours it by calling `LoginTokens.redeem(request)` early in its login handling: when that returns a user name, the application logs that user in as it does after a successful password check, so the page's own later requests carry the login. The call makes every check itself. For example, a servlet filter for authentication that keeps the user in the session:
    ```
     public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain)
         throws IOException, ServletException
     {
         HttpServletRequest request = (HttpServletRequest) req;
    
         // The server's browser, opening a report page as a user: log that user in
         String tokenUser = LoginTokens.redeem(request);
         if (tokenUser != null) request.getSession(true).setAttribute(USER, tokenUser);
    
         HttpSession session = request.getSession(false);
         String user = session == null ? null : (String) session.getAttribute(USER);
         if (user == null) {
             ((HttpServletResponse) res).sendError(HttpServletResponse.SC_UNAUTHORIZED);
             return;
         }
         // the logged-in user, as SmartClient reads it from the request
         Principal principal = () -> user;
         chain.doFilter(new HttpServletRequestWrapper(request) {
             public String getRemoteUser() { return user; }
             public Principal getUserPrincipal() { return principal; }
         }, res);
     }
     
    ```
    With Spring Security, make the same call in a filter placed before Spring's login handling, and for the user it returns, load that user's details and save an authenticated token for them in the security context and its session, as a form login does;
*   a report whose content does not depend on who views it needs none of this: without a login the page is rendered with no user. Keep `reportDelivery.requireLogin` on all the same, so only signed-in users can share and schedule.

Login tokens are issued and honoured only while `authentication.loginTokens.enabled` is on (by default, whenever `reportDelivery.enabled` is), and are accepted only from `authentication.loginTokens.allowedAddresses` (by default this machine; add a reverse proxy's address if renders reach the application through one).

**In the report**

The report's toolbar offers Share Now, Schedule Delivery ([ReportToolbar.showScheduleDelivery](../classes/ReportToolbar.md#attr-reporttoolbarshowscheduledelivery)) and Manage Schedules ([ReportToolbar.showManageSchedules](../classes/ReportToolbar.md#attr-reporttoolbarshowmanageschedules)) only where the server supports them and the current user may use them. The Schedule dialog sets the cadence with a [SchedulerItem](../classes/SchedulerItem.md#class-scheduleritem): daily, on chosen weekdays or on a day of the month, at any time in 15-minute steps, in a chosen time zone. Manage Schedules lists the user's schedules of the report (or of all their reports) to edit, pause, resume or delete. [DataReport.scheduleRecipientOptions](../classes/DataReport.md#attr-datareportschedulerecipientoptions) suggests recipients and [DataReport.scheduleTimeZones](../classes/DataReport.md#attr-datareportscheduletimezones) narrows the time zones offered.

**Rendering a report to a file**

A report is named by the path of its report page on this server, for example `/tools/visualBuilder/projectRunner.jsp?type=project&project=Sales` in Reify or `/tools/reporting/reportPage.jsp?report=Sales` without it. The server adds the origin itself (`reportRender.baseUrl`), so a caller never chooses which host the server's browser visits, and the path must be a report page (`reportRender.reportPathPattern`; see _Report pages_ under _Delivery outside Reify_). The server opens the page in headless Chrome and the report renders itself: the snapshot, the data behind each component and the print layout all come from the live page, and Excel and PDF are built inside the page's own request, so the viewer's security and field masking apply exactly as on screen.

*   From server code: `com.isomorphic.rpc.ReportRenderer.render(reportPath, formats, options)` returns the files produced (formats `png`, `xlsx`, `pdf`) and the reason for any that could not be.
*   From the client: `downloadFile` on the `rb_report_renders` DataSource, with criteria `reportPath` and `format`, streams the file. It renders as the requesting user.

**The schedule contract: `rb_scheduled_reports`**

`add` schedules a delivery, `update` changes or pauses one, `remove` cancels one. Fields a caller provides:

| deployedUrl | required: the report's published page path, as above. Stored normalized, as a browser would request it. |
|---|---|
| cronExpression | required: when to deliver, as a 5-field Unix cron expression (minute, hour, day of month, month, day of week; Sunday is 0 or 7). |
| timezone | the IANA time zone the cron expression is read in, e.g. America/New_York; default the server's. |
| recipients | required: email addresses separated by commas or semicolons. |
| subject, message | the email's subject and cover note. |
| attachFormats | files attached besides the inline snapshot: any of xlsx, pdf. |
| status | active (default) or paused; the server sets error when it cannot schedule a row. |
| reportFileName, reportTitle | the report's name and the title shown in the email. |

`frequency`, `daysOfWeek`, `sendTime` and `skin` are kept for the Schedule dialog to show a schedule again; delivery uses only the cron expression and time zone. The server writes `lastRunDate`, `lastRunStatus` (`success`, `partial` — sent without something requested, with the reason in `lastRunMessage` — or `error`, nothing sent), `lastRunMessage`, `nextRunDate`, `createdBy` and `createdDate`; values a client sends for them are ignored.

A save is refused with a validation error on the field concerned when the cron expression is invalid or would ever deliver more often than every `reportScheduler.minIntervalMinutes` (default 60), the time zone is unknown, the path is not a report page, or the recipients are malformed, too many (`reportDelivery.maxRecipients`, default 25) or outside `reportDelivery.allowedRecipientDomains` when that is set.

**Deliver now: `rb_report_delivery_runs`**

An `add` naming a `scheduleId` delivers that schedule immediately, paused or not, and records the outcome on its row, exactly as a scheduled run does. The response carries `status` (`success`, `partial` or `error`) and `message`. The schedule is read as the caller, so a user can deliver only their own schedules.

**Driving delivery from your own scheduler**

Leave `reportScheduler.builtInTrigger` off and either:

*   store schedules in `rb_scheduled_reports` and, on your scheduler's timetable, call "deliver now" for each one due. Without the built-in trigger, `nextRunDate` is the next time a schedule's cron expression matches in its time zone, and a delivery moves it on, so "due" is simply an active schedule whose `nextRunDate` has passed. From server code in the same application, use DSRequests marked `setClientRequest(false)`: server requests are trusted, as for declarative security, and need no logged-in user. Over HTTP, call as a logged-in user;
*   or call `ReportRenderer.render()` directly and send the files your own way.

The examples below are the code of the framework's own tests for these routes.

_A tick of your scheduler_: delivers every schedule that is due, and returns each delivery's outcome. `criteria` narrows which schedules a tick considers (null for all), for a deployment that partitions its schedules.

```
 public static List<Map> deliverDue(Map criteria, Date asOf) throws Exception {
     Map where = new HashMap();
     if (criteria != null) where.putAll(criteria);
     where.put("status", "active");
     DSRequest fetch = new DSRequest("rb_scheduled_reports", "fetch");
     fetch.setCriteria(where);
     fetch.setClientRequest(false);   // server code is trusted: no login needed

     List<Map> outcomes = new ArrayList<Map>();
     for (Object row : fetch.execute().getDataList()) {
         Map schedule = (Map) row;
         Date due = (Date) schedule.get("nextRunDate");
         if (due == null || due.after(asOf)) continue;

         DSRequest run = new DSRequest("rb_report_delivery_runs", "add");
         Map values = new HashMap();
         values.put("scheduleId", schedule.get("scheduleId"));
         run.setValues(values);
         run.setClientRequest(false);
         // { scheduleId, status: "success" | "partial" | "error", message }
         outcomes.add(run.execute().getDataMap());
     }
     return outcomes;
 }
 
```
Call it on any timetable your application already has, for example every five minutes from a `java.util.concurrent.ScheduledExecutorService` (or a Spring `@Scheduled` method):
```
 executor.scheduleAtFixedRate(() -> {
     try { deliverDue(null, new Date()); }
     catch (Exception e) { log.warn("Report delivery tick failed", e); }
 }, 0, 5, TimeUnit.MINUTES);
 
```
A tick never sends a schedule twice for one due time, but two ticks running at once could, so run one tick at a time (a cluster should run ticks on one server only).

_An operating-system scheduler (cron)_: expose the tick through a small endpoint that only your scheduler can call, so the schedule work still runs as trusted server code. Here a servlet requires a POST carrying a shared key from your server configuration:

```
 protected void doPost(HttpServletRequest request, HttpServletResponse response)
         throws IOException
 {
     String key = Config.getGlobal().getString("myApp.reportTick.key"),
            sent = request.getHeader("X-Tick-Key");
     if (key == null || key.isEmpty() || sent == null ||
         !MessageDigest.isEqual(key.getBytes(StandardCharsets.UTF_8),
                                sent.getBytes(StandardCharsets.UTF_8)))
     {
         response.sendError(HttpServletResponse.SC_FORBIDDEN);
         return;
     }
     try {
         List<Map> outcomes = deliverDue(null, new Date());
         response.setContentType("application/json");
         response.getWriter().print(JSTranslater.get().toJS(
             Collections.singletonMap("outcomes", outcomes)));
     } catch (Exception e) {
         throw new IOException(e);
     }
 }
 
```
and the crontab entry calls it every five minutes, with the key kept out of the URL (and so out of access logs):
```
 */5 * * * * curl -fsS -X POST -H "X-Tick-Key: $KEY" https://example.com/tick
 
```

_Rendering a report yourself_: renders the report at `reportPath` as user `runAs` (null: no logged-in user) and emails the PDF with `com.isomorphic.mail.MailMessage`.

```
 Map options = new HashMap();
 if (runAs != null) options.put("runAs", runAs);
 ReportRenderer.Result result =
     ReportRenderer.render(reportPath, Arrays.asList("pdf"), options);

 ReportRenderer.Rendered pdf = result.files.get("pdf");
 if (pdf == null) throw new Exception("No PDF: " + result.problems);
 MailMessage mail = new MailMessage();
 mail.addRecipients(recipients);
 mail.setSubject("Your report");
 mail.setBody("The report is attached.");
 ByteArrayDataSource attachment = new ByteArrayDataSource(pdf.bytes, pdf.mimeType);
 attachment.setName(pdf.fileName);
 mail.addAttachment(attachment);
 mail.send();
 
```
In a database with per-user or per-organization sandboxes, a server fetch reads only the database the request is for, so a tick must run once for each sandbox holding schedules; the built-in scheduler does this itself.

**The built-in scheduler (demonstration only)**

With `reportScheduler.builtInTrigger: true`, every active schedule gets a job in this server's Quartz instance (see `quartz.properties`), re-created when the server starts. Jobs are held in memory and each server of a cluster would fire every schedule, so this suits a single-server demonstration, not production.

**Security**

*   Sharing and scheduling require a logged-in user (`reportDelivery.requireLogin`, default true — set false for an application without authentication) and, when `reportDelivery.requiredRole` is set, that role. `reportDelivery.disableOnRequestAttribute` names a request attribute that turns delivery off where it is set, for contexts whose readers should not share or schedule the report.
*   Schedules belong to the user who saved them: each user sees and changes only their own. Schedules saved where no one was logged in have no owner; users in `reportDelivery.adminRole` (default `reportAdmin`; a superuser has every role) reach them through the `ownerlessFetch` and `ownerlessRemove` operations.
*   A scheduled delivery renders the report as its schedule's owner. Behind a login page, the server's browser is logged in with a one-time token for that user and page, and visits `reportRender.logoutPath` afterwards to end the session.
*   Each user may send at most `reportDelivery.maxPerUserPerDay` report emails (default 50) in any 24 hours; Share Now counts against the sender and scheduled deliveries against the schedule's owner. Every email sent is recorded in the server-only `rb_delivery_log` DataSource.
*   Renders are limited, since each runs its own Chrome. At most `reportRender.maxConcurrent` run at once on a server (default 3); another waits up to `reportRender.maxWaitSeconds` (default 120) for one to finish and is then refused as busy (`ReportRenderer.BusyException` to server code). A file a user requests is also limited per user: `reportRender.maxConcurrentPerUser` renders in progress at once (default 1) and `reportRender.maxPerUserPerHour` in any hour (default 20), counted by client address where no one is logged in. Deliveries, which count against the daily email limit, and renders started by server code are not limited per user. 0 turns any of these limits off.
*   Emails link to the live report at `reportDelivery.publicUrl` (by default `reportRender.baseUrl`); set `reportDelivery.includeLiveLink: false` when recipients cannot open the report page.

**Sandboxed databases**

In a database with per-user or per-organization sandboxes, schedules live in the sandbox of the user who saved them, with the rest of that user's content; the built-in scheduler runs each job in its schedule's sandbox and, on startup, restores schedules from every sandbox except those matching `reportScheduler.skipSandboxPattern`. Place `rb_delivery_log` in an unsandboxed database so the daily limit counts across sandboxes.

### Related

- [SchedulerItem.describeCron](../classes/SchedulerItem.md#classmethod-scheduleritemdescribecron)
- [DataReport.setReportPageURL](../classes/DataReport.md#method-datareportsetreportpageurl)
- [SchedulerItem.scheduleChanged](../classes/SchedulerItem.md#method-scheduleritemschedulechanged)
- [SchedulerItem.getScheduleValue](../classes/SchedulerItem.md#method-scheduleritemgetschedulevalue)
- [SchedulerItem.setScheduleValue](../classes/SchedulerItem.md#method-scheduleritemsetschedulevalue)
- [SchedulerItem.describeSchedule](../classes/SchedulerItem.md#method-scheduleritemdescribeschedule)
- [ReportBuilder.setReportPageURL](../classes/ReportBuilder.md#method-reportbuildersetreportpageurl)
- [SchedulerItem](../classes/SchedulerItem.md#class-scheduleritem)
- [DataReport.scheduleRecipientOptions](../classes/DataReport.md#attr-datareportschedulerecipientoptions)
- [DataReport.scheduleTimeZones](../classes/DataReport.md#attr-datareportscheduletimezones)
- [DataReport.reportPageURL](../classes/DataReport.md#attr-datareportreportpageurl)
- [ReportToolbar.showScheduleDelivery](../classes/ReportToolbar.md#attr-reporttoolbarshowscheduledelivery)
- [ReportToolbar.showManageSchedules](../classes/ReportToolbar.md#attr-reporttoolbarshowmanageschedules)
- [SchedulerItem.minuteIncrement](../classes/SchedulerItem.md#attr-scheduleritemminuteincrement)
- [SchedulerItem.maxDayOfMonth](../classes/SchedulerItem.md#attr-scheduleritemmaxdayofmonth)
- [SchedulerItem.timeZones](../classes/SchedulerItem.md#attr-scheduleritemtimezones)
- [ReportBuilder.reportPageURL](../classes/ReportBuilder.md#attr-reportbuilderreportpageurl)

---
