# Consulta CNPJ em Lote — Brazil CNPJ Bulk Lookup — Python, Node.js & cURL examples

Look up **thousands of Brazilian CNPJs** in one run and get one clean row per company from the **Receita Federal open CNPJ data**: razão social, nome fantasia, **situação cadastral**, opening date, main and secondary **CNAE**, address, **e-mail and phone**, porte, capital social, natureza jurídica, **Simples Nacional / MEI** and the partners (**QSA**). Three free public mirrors (OpenCNPJ → Minha Receita → BrasilAPI) with **automatic fallback**, check-digit validation (alphanumeric CNPJ included), 8-digit roots and duplicates handled. **$0.80 per 1,000 companies**; invalid and not-found CNPJs are free.

Hosted on Apify: **[Consulta CNPJ em Lote — Brazil CNPJ Bulk Lookup](https://apify.com/tidydata/brazil-cnpj-lookup?fpr=wtg6qt)**. These examples show how to call it from your code; the Actor runs in the cloud, no API key for the source site, no proxies to manage.

## Python

```bash
pip install apify-client
export APIFY_TOKEN=...   # free account at apify.com → Settings → API & Integrations
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("tidydata/brazil-cnpj-lookup").call(run_input={
    "cnpjs": [
        "33.000.167/0001-01",
        "00.000.000/0001-91",
        "60.701.190/0001-04"
    ],
    "includePartners": True
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print({k: item.get(k) for k in ['cnpjFormatted', 'companyName', 'status', 'mainCnaeFormatted', 'city', 'state', 'email', 'partnersCount']})
```

## Node.js

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('tidydata/brazil-cnpj-lookup').call({"cnpjs": ["33000167000101"]});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items.length, items[0]);
```

## cURL (one call, results as JSON)

```bash
curl -s -X POST "https://api.apify.com/v2/acts/tidydata~brazil-cnpj-lookup/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"cnpjs": ["33000167000101"]}'
```

## More TidyData Actors

[YouTube Transcript](https://apify.com/tidydata/youtube-transcript-scraper?fpr=wtg6qt) · [YouTube Comments](https://apify.com/tidydata/youtube-comments-scraper?fpr=wtg6qt) · [YouTube Scraper](https://apify.com/tidydata/youtube-channel-scraper?fpr=wtg6qt) · [Website Contacts](https://apify.com/tidydata/website-contact-extractor?fpr=wtg6qt) · [Google News](https://apify.com/tidydata/google-news-scraper?fpr=wtg6qt) · [App Reviews](https://apify.com/tidydata/app-reviews-scraper?fpr=wtg6qt) · [Merge & Dedupe](https://apify.com/tidydata/merge-dedupe-datasets?fpr=wtg6qt) · [all of them](https://github.com/tidydata-dev)

Examples are MIT-licensed.

---
<sub>Links to apify.com include our affiliate ID: if you start a paid Apify plan through them, Apify pays TidyData a commission at no extra cost to you.</sub>
