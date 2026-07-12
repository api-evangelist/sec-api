# SEC API (sec-api)

SEC API (sec-api.io) is a commercial developer platform that turns the U.S. Securities and Exchange Commission's EDGAR system into a fast, queryable REST and real-time streaming API. It covers 18+ million filings back to 1993 across 400+ EDGAR form types, with a Lucene-based Filing Query API, a Full-Text Search API over filing bodies and exhibits since 2001, an XBRL-to-JSON financial statement converter, a section Extractor for 10-K/10-Q/8-K, and structured datasets for insider trading (Form 3/4/5), institutional holdings (Form 13F), 13D/13G, Form D, Form ADV, IPOs, and more. A real-time Filing Stream API pushes newly published filings to clients over a WebSocket connection as soon as they hit EDGAR.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/sec-api/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/sec-api/refs/heads/main/apis.yml)

## Access Model

SEC API is a **commercial, closed-source** service that sits in front of the SEC's own free, public EDGAR data. The underlying filings are public record; sec-api.io's value is the normalized query, full-text, XBRL-parsing, structured-dataset, and real-time streaming layer on top of them.

- **Authentication:** a single API token, obtained from your sec-api.io account. Pass it either as an `Authorization: YOUR_API_KEY` header or as a `?token=YOUR_API_KEY` query parameter. The real-time stream uses `wss://stream.sec-api.io?apiKey=YOUR_API_KEY`.
- **Free trial:** 100 API calls, one-time, no credit card, for evaluation.
- **Paid tiers:** Personal & Startups ($55/mo, or $49/mo billed annually) and Business Internal Use ($239/mo, or $199/mo billed annually), plus a custom Enterprise tier with redistribution licensing. See `plans/sec-api-plans-pricing.yml`.
- **Rate limits:** governed per plan (for example 20 requests/second on the Query API for Personal, 40 requests/second for Business). See `rate-limits/sec-api-rate-limits.yml`.

This entry documents the public, published surface of the API from sec-api.io's own developer docs. Endpoint paths, request shapes, and pricing were grounded against the live documentation on 2026-07-11; verify current numbers against the sec-api.io pricing and docs pages before relying on them.

## Tags

- SEC Filings
- Regulatory Filings
- EDGAR
- Financial Data
- Compliance
- Government Reports
- Insider Trading
- 13F
- XBRL
- Full-Text Search

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### SEC API Filing Query API

Search and filter 18+ million EDGAR filings (1993-present) across 400+ form types using Lucene syntax over filing metadata - form type, ticker, CIK, company name, filing date, and more. POST a query to receive matching filing metadata with document URLs, entities, and data files.

- **Human URL:** [https://sec-api.io/docs/query-api](https://sec-api.io/docs/query-api)
- **Base URL:** `https://api.sec-api.io`

#### Tags

- SEC Filings
- EDGAR
- Regulatory Filings
- Filing Search

#### Properties

- [Documentation](https://sec-api.io/docs)
- [API Reference](https://sec-api.io/docs/query-api)
- [OpenAPI](openapi/sec-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sec-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sec-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### SEC API Full-Text Search API

Keyword and phrase search across the full text of all EDGAR filings and their exhibits published since 2001, with wildcard and Boolean operators, form-type and CIK filters, and date-range scoping. Returns filing metadata and document URLs for every matching document.

- **Human URL:** [https://sec-api.io/docs/full-text-search-api](https://sec-api.io/docs/full-text-search-api)
- **Base URL:** `https://api.sec-api.io`

#### Tags

- Full-Text Search
- Regulatory Filings
- Government Reports
- EDGAR

#### Properties

- [API Reference](https://sec-api.io/docs/full-text-search-api)
- [OpenAPI](openapi/sec-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sec-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sec-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### SEC API Filing Stream API

Real-time, push-based WebSocket feed of newly published SEC EDGAR filings. Connect to `wss://stream.sec-api.io` with an API key and receive a stringified JSON array of filing metadata objects the moment each new filing is released, typically within 300 milliseconds of publication.

- **Human URL:** [https://sec-api.io/docs/stream-api](https://sec-api.io/docs/stream-api)
- **Base URL:** `wss://stream.sec-api.io`

#### Tags

- Real-Time
- Streaming
- WebSocket
- EDGAR

#### Properties

- [Documentation](https://sec-api.io/docs/stream-api)
- [AsyncAPI](asyncapi/sec-api-asyncapi.yml) — [AsyncAPI Specification](https://www.asyncapi.com/docs/reference/specification/latest)

### SEC API XBRL-to-JSON Converter API

Converts the XBRL financial data embedded in 10-K, 10-Q, and other filings into standardized JSON - income statement, balance sheet, cash flow, cover page, and custom items - addressable by filing HTM URL, XBRL URL, or accession number via a simple GET request.

- **Human URL:** [https://sec-api.io/docs/xbrl-to-json-converter-api](https://sec-api.io/docs/xbrl-to-json-converter-api)
- **Base URL:** `https://api.sec-api.io`

#### Tags

- XBRL
- Financial Data
- Financial Statements
- Regulatory Filings

#### Properties

- [API Reference](https://sec-api.io/docs/xbrl-to-json-converter-api)
- [OpenAPI](openapi/sec-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sec-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sec-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### SEC API Extractor API

Extracts individual textual sections (items) from 10-K, 10-Q, and 8-K filings - for example 10-K Item 1A Risk Factors or Item 7 MD&A - returning clean plain text or lightly formatted HTML for a given filing URL and item identifier.

- **Human URL:** [https://sec-api.io/docs/sec-filings-item-extraction-api](https://sec-api.io/docs/sec-filings-item-extraction-api)
- **Base URL:** `https://api.sec-api.io`

#### Tags

- Text Extraction
- Regulatory Filings
- Government Reports
- 10-K

#### Properties

- [API Reference](https://sec-api.io/docs/sec-filings-item-extraction-api)
- [OpenAPI](openapi/sec-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sec-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sec-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### SEC API Insider Trading API

Structured, queryable insider transaction data parsed from SEC Form 3, 4, and 5 filings - issuer, reporting owner and relationship, non-derivative and derivative transactions, prices, share counts, post-transaction holdings, and footnotes - searchable with Lucene syntax over any field.

- **Human URL:** [https://sec-api.io/docs/insider-ownership-trading-api](https://sec-api.io/docs/insider-ownership-trading-api)
- **Base URL:** `https://api.sec-api.io`

#### Tags

- Insider Trading
- Regulatory Filings
- Financial Data
- Compliance

#### Properties

- [API Reference](https://sec-api.io/docs/insider-ownership-trading-api)
- [OpenAPI](openapi/sec-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sec-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sec-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### SEC API Form 13F Holdings API

Quarterly portfolio holdings of institutional investment managers disclosed in Form 13F filings, exposed as two endpoints - holdings information tables (CUSIP, ticker, shares, value per position) and cover pages - both searchable with Lucene queries over accession number, manager, and filing date.

- **Human URL:** [https://sec-api.io/docs/form-13-f-filings-institutional-holdings-api](https://sec-api.io/docs/form-13-f-filings-institutional-holdings-api)
- **Base URL:** `https://api.sec-api.io`

#### Tags

- 13F
- Institutional Holdings
- Financial Data
- Regulatory Filings

#### Properties

- [API Reference](https://sec-api.io/docs/form-13-f-filings-institutional-holdings-api)
- [OpenAPI](openapi/sec-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/sec-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/sec-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Domain Security](security/sec-api-domain-security.yml)
- [Authentication](authentication/sec-api-authentication.yml)
- [LinkedIn](https://www.linkedin.com/company/sec-api-io)
- [Website](https://sec-api.io)
- [Documentation](https://sec-api.io/docs)
- [Plans](plans/sec-api-plans-pricing.yml)
- [Rate Limits](rate-limits/sec-api-rate-limits.yml)
- [Fin Ops](finops/sec-api-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
