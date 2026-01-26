# Full Text Search

[← Back to API Index](../reference.md)

---

## KB Topic: Full Text Search

### Description
Full Text Search (FTS) enables searching the content of documents stored in binary fields, rather than just metadata fields. When enabled on a DataSource, textual search operators (contains, iContains, startsWith, etc.) applied to FTS-eligible binary fields will automatically trigger full-text search through a configured provider.

**Enabling Full Text Search**

FTS is enabled by adding a `<fullTextSearch>` element to your DataSource definition:

```
 <DataSource ID="documents">
   <fullTextSearch provider="openSearch"/>
   <fields>
     <field name="id" type="sequence" primaryKey="true"/>
     <field name="docFile" type="binary"/>
   </fields>
 </DataSource>
 
```

With this configuration, any fetch request that includes textual criteria on the "docFile" field will trigger an FTS query against the configured provider (OpenSearch or Elasticsearch in this example).

**How FTS Works**

When a fetch request includes textual search operators on an FTS-eligible binary field:

1.  The framework detects this as an FTS trigger
2.  A query is sent to the FTS provider (OpenSearch, Elasticsearch, or Oracle Text)
3.  The provider returns matching document IDs and relevance metadata (score, snippets)
4.  The original criteria is modified to include a primary key restriction to only those IDs
5.  The normal database fetch executes with the modified criteria
6.  FTS metadata (scores, snippets) is merged into the response records

**Supported Search Operators**

The following operators trigger FTS when applied to an FTS-eligible binary field:

*   **contains/iContains**: Match documents containing the search term(s)
*   **startsWith/iStartsWith**: Match documents with terms starting with the value
*   **endsWith/iEndsWith**: Match documents with terms ending with the value
*   **equals/iEquals**: Exact term match

Additionally, FTS-specific operators are available for advanced searching:

*   **phrase/iPhrase**: Match an exact phrase (words in order)
*   **near/iNear**: Proximity search - match terms within a certain distance
*   **fuzzy/iFuzzy**: Approximate matching with edit distance tolerance
*   **prefixMatch/iPrefixMatch**: Match terms starting with the given prefix

The "i" prefix variants perform case-insensitive matching.

**FTS Providers**

Two types of FTS providers are supported:

*   **External providers** (OpenSearch, Elasticsearch): These use a separate search engine that maintains its own full-text index. Results are fetched via a provider DataSource and merged with the primary fetch.
*   **Oracle Text**: A special case that generates CONTAINS() and SCORE() SQL predicates directly, with no separate provider query.

Configure providers in server.properties:

```
 # Default provider when not specified in DataSource
 fullText.defaultProvider=openSearch

 # List of available providers
 fullText.providers=oracleText,openSearch

 # External provider configuration
 fullText.provider.openSearch.dataSourceID=FTSOpenSearch
 fullText.openSearch.endpoint=http://localhost:9200

 # Oracle Text is built-in (no external DataSource)
 fullText.provider.oracleText.type=oracleText
 
```

**FTS Result Fields**

When FTS is enabled, the following fields are automatically generated on the DataSource to receive FTS metadata:

*   **fts\_score**: Relevance score from the search engine (float)
*   **fts\_snippet**: A highlighted snippet showing match context (text)
*   **fts\_snippets**: Multiple snippets if document has multiple matches (JSON array)
*   **fts\_highlights**: Highlighted field contents showing match locations (JSON object)
*   **fts\_rank**: Result rank within the search results (integer)
*   **fts\_providerMeta**: Provider-specific metadata (JSON)

The field name prefix can be customized via the resultFieldPrefix attribute.

**Field-Level Configuration**

Individual binary fields can be excluded from FTS or assigned different providers:

```
 <field name="docFile" type="binary"/>
 <field name="thumbnail" type="binary" fullTextSearch="false"/>
 <field name="archiveFile" type="binary" fullTextProvider="oracleText"/>
 
```

**Error Handling**

FTS errors can be handled according to policy (set on provider or DataSource):

*   **fail** (default): FTS errors cause the request to fail
*   **warnAndIgnore**: Log warning and continue without FTS results
*   **ignore**: Silently continue without FTS results

**API Access**

Server-side code can access the original criteria (before FTS modification) via DSRequest.getOriginalCriteria(). FTS metadata can also be accessed via DSRequest.getMergeData().

---
