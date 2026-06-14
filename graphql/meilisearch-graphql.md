# Meilisearch GraphQL Schema

This is a conceptual GraphQL schema for the [Meilisearch](https://www.meilisearch.com/) open-source search engine API. It maps the Meilisearch REST API surface to GraphQL types, queries, and mutations.

## Source

- API Reference: https://www.meilisearch.com/docs/reference/api
- GitHub: https://github.com/meilisearch/meilisearch

## Schema File

[meilisearch-schema.graphql](meilisearch-schema.graphql)

## Type Overview

### Index Types

| Type | Description |
|------|-------------|
| `Index` | A search index holding a collection of documents |
| `IndexDetails` | Extended metadata including document count and field distribution |
| `IndexSettings` | All configurable settings for an index |
| `IndexStats` | Runtime statistics (document count, indexing status) |
| `IndexStatus` | Enum: `available`, `unavailable`, `loading` |

### Field & Attribute Types

| Type | Description |
|------|-------------|
| `Field` | A field descriptor within an index |
| `FilterableAttributes` | Attributes usable in filters and facets |
| `SortableAttributes` | Attributes that support sort operations |
| `SearchableAttributes` | Attributes included in full-text search |
| `DisplayedAttributes` | Attributes returned in search results |
| `StopWords` | Words ignored during indexing and search |
| `Synonyms` / `SynonymEntry` | Synonym mappings for an index |

### Search Configuration Types

| Type | Description |
|------|-------------|
| `TypoTolerance` | Typo tolerance configuration |
| `MinWordSizeForTypos` | Word length thresholds for typo correction |
| `Faceting` | Facet value limits and ordering |
| `Pagination` | Maximum total hits constraint |
| `Proximity` | Proximity precision mode |

### Document Types

| Type | Description |
|------|-------------|
| `Document` | A single stored document |
| `DocumentDetails` | Document with index context |

### Search Result Types

| Type | Description |
|------|-------------|
| `SearchResult` | Paginated search response with hits and metadata |
| `Hit` | A single matched document with scores and formatting |
| `SearchHits` | All hits with total count |
| `FacetDistribution` | Distribution of values across facets |
| `FacetDetails` | Details for a single facet field |
| `FacetValue` | A facet value with document count |
| `TotalHits` | Exact or estimated total hit count |
| `ProcessingTimeMs` | Query processing time |

### Search Query Input Types

| Type | Description |
|------|-------------|
| `SearchQuery` | Full search request parameters |
| `SearchFilter` | Filter expression |
| `SearchFacets` | Facets to compute |
| `SearchSort` | Sort directive |
| `HybridSearchInput` | Vector + keyword hybrid search parameters |

### Highlighting & Cropping

| Type | Description |
|------|-------------|
| `Highlight` | Highlighted snippet for a matched attribute |
| `CropPosition` | Crop position for a matched attribute |

### Vector / Embedder Types

| Type | Description |
|------|-------------|
| `EmbedderConfig` | Embedder configuration for vector search |
| `VectorSearch` | Vector search result with semantic scores |

### Task Types

| Type | Description |
|------|-------------|
| `Task` | An asynchronous task |
| `TaskDetails` | Task-type-specific detail payload |
| `TaskType` | Enum of all task categories |
| `TaskStatus` | Enum: `enqueued`, `processing`, `succeeded`, `failed`, `canceled` |
| `TaskError` | Error information for failed tasks |
| `TaskQueue` | Paginated list of tasks |
| `TaskCancellation` | Result of a cancellation request |

### Key / Auth Types

| Type | Description |
|------|-------------|
| `Key` | An API key with scoped permissions |
| `KeyDetails` | Detailed API key view |
| `KeyAction` | Enum of all permission actions |
| `KeyIndex` | Index scope pattern for a key |

### Batch Types

| Type | Description |
|------|-------------|
| `Batch` | A batch of tasks processed together |
| `BatchDetails` | Task summary counters for a batch |
| `BatchStats` | Per-status task counts in a batch |
| `BatchStatus` | Enum: `succeeded`, `failed`, `canceled`, `processing` |

### Settings & Update Types

| Type | Description |
|------|-------------|
| `Settings` | Global settings wrapper |
| `SettingsDetails` | Settings update result with task reference |
| `UpdateStatus` | Status of an update operation |

### Stats & Diagnostics

| Type | Description |
|------|-------------|
| `Stats` | Instance-wide statistics |
| `DatabaseSize` | Database size information |
| `Health` | Instance health status |
| `Version` | Meilisearch version info |

### Federated Search Types

| Type | Description |
|------|-------------|
| `FederatedSearchQuery` | Multi-index search input |
| `FederationOptions` | Federated search merging options |
| `FederatedSearchResult` | Merged results from multiple indexes |
| `FederatedHit` | A hit with its source index uid |

### Experimental Features

| Type | Description |
|------|-------------|
| `ExperimentalFeatures` | Feature flags for the instance |

### Error Types

| Type | Description |
|------|-------------|
| `ErrorCode` | Enum of all Meilisearch error codes |
| `Error` | Structured API error response |

## Queries

| Query | Description |
|-------|-------------|
| `indexes` | List all indexes |
| `index(uid)` | Get a single index |
| `indexSettings(indexUid)` | Get settings for an index |
| `indexStats(indexUid)` | Get stats for an index |
| `documents(indexUid, ...)` | List documents in an index |
| `document(indexUid, documentId)` | Get a single document |
| `search(indexUid, query)` | Perform a search |
| `federatedSearch(query)` | Multi-index federated search |
| `tasks(...)` | List tasks with filters |
| `task(uid)` | Get a single task |
| `batches(...)` | List batches |
| `batch(uid)` | Get a single batch |
| `keys(...)` | List API keys |
| `key(uid)` | Get a single API key |
| `stats` | Instance-wide statistics |
| `health` | Instance health |
| `version` | Meilisearch version |
| `experimentalFeatures` | Experimental feature flags |

## Mutations

| Mutation | Description |
|----------|-------------|
| `createIndex` | Create a new index |
| `updateIndex` | Update an index |
| `deleteIndex` | Delete an index |
| `swapIndexes` | Swap index pairs |
| `addDocuments` | Add or replace documents |
| `updateDocuments` | Add or update documents |
| `deleteAllDocuments` | Delete all documents in an index |
| `deleteDocumentsByFilter` | Delete documents matching a filter |
| `deleteDocuments` | Delete specific documents by id |
| `editDocuments` | Edit documents by function (experimental) |
| `updateSettings` | Update index settings |
| `resetSettings` | Reset settings to defaults |
| `cancelTasks` | Cancel matching tasks |
| `deleteTasks` | Delete matching tasks |
| `createKey` | Create an API key |
| `updateKey` | Update an API key |
| `deleteKey` | Delete an API key |
| `createDump` | Trigger a database dump |
| `createSnapshot` | Trigger a snapshot |
| `updateExperimentalFeatures` | Update experimental feature flags |

## Key Features Represented

- Full index lifecycle management (create, update, delete, swap)
- Document CRUD with primary key configuration
- Rich search with filtering, faceting, sorting, pagination, and highlighting
- Hybrid (vector + keyword) search via embedder configuration
- Federated search across multiple indexes
- Asynchronous task queue with batch tracking
- Fine-grained API key management with action and index scoping
- Instance statistics, health, and version diagnostics
- Experimental features flag management
