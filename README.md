## BloodHound Query Legacy to CE Tool

### Convert and Upload Custom Queries from BloodHound Legacy to BloodHound CE

This tool simplifies the process of migrating/converting your Cypher queries from **Legacy BloodHound** to **BloodHound CE (Community Edition)**. It automatically reformats legacy custom queries into the new BloodHound CE format and uploads them directly through the BloodHound CE API.

### Key Features
- Convert BloodHound Legacy queries to the BloodHound CE JSON format.
- Automatically upload reformatted queries to BloodHound CE via API.
- Support for rate-limited uploading to prevent API blocking.
- Detailed error handling and progress reporting during query uploads.

**Update 12/01/2025 - Improved Script Features:**
- Missing `category` is set to `null` automatically instead of causing an error.
- Missing query `name` is assigned a unique name in the format: `Unnamed query <uuid>`.
- Queries with missing or empty query values are skipped with a message indicating why.

### Quick Demo

![bh_upload_queries](https://github.com/user-attachments/assets/a6d6bce1-749d-4d72-bade-a5b10bf2b0b7)

### Table of Contents

1.  [Usage](#usage)
2.  [Getting the JWT Token from BloodHound CE](#getting-the-jwt-token-from-bloodhound-ce)
3.  [Old vs New Query Format](#old-vs-new-query-format)
4.  [Support & Contribution](#support--contribution)
5.  [Credits](#credits)
6.  [License](#license)

## Usage

1.  [Install Prerequisites](#1-install-prerequisites)
2.  [Usage Examples](#2-usage-examples)

### 1\. Install Prerequisites

Make sure you have Python 3 installed on your system, along with the following Python libraries:

```bash
pip install requests argparse
```

Download the python script here:
- [bh_query_legacy2ce.py](https://github.com/WafflesExploits/Bloodhound-query-legacy2ce/blob/main/bh_query_legacy2ce.py)

### 2\. Usage Examples

1.  [Convert and Upload Custom Queries](#convert-and-upload-custom-queries)
2.  [Convert Only (Save to File Without Uploading)](#convert-only-save-to-file-without-uploading)
3.  [Upload to a Different BloodHound CE API URL](#upload-to-a-different-bloodhound-ce-api-url)

#### Convert and Upload Custom Queries

This command converts custom queries from the Legacy BloodHound format and uploads them directly to BloodHound CE using your JWT token.

```bash
python upload_bloodhound_queries.py --input-file bloodhound_legacy_customqueries.json --jwt-token YOUR_JWT_TOKEN
```

#### Convert Only (Save to File Without Uploading)

This command converts custom queries without uploading them. The output is saved to a file in the new BloodHound CE format.

```bash
python upload_bloodhound_queries.py --input-file bloodhound_legacy_customqueries.json --convert-only --output-file newformat_customqueries.json
```

#### Upload to a Different BloodHound CE API URL

By default, the tool uses `http://localhost:8080/api/v2/saved-queries` as the API endpoint. If your BloodHound CE instance runs on a different port or URL, use the `--api-url` flag to customize:

```bash
python upload_bloodhound_queries.py --input-file newformat_customqueries.json \
                                    --jwt-token YOUR_JWT_TOKEN \
                                    --api-url "http://your-server:your-port/api/v2/saved-queries"
```

## Getting the JWT Token from BloodHound CE

To upload queries via the API, you'll need the **JWT token** from BloodHound CE. Here's how to get it:

1.  Open BloodHound CE and navigate to the **API Explorer**.
2.  Find the **Get Self** API request, click **Try It Out**, then **Execute**.
    - <img src="https://github.com/user-attachments/assets/b429256d-2b14-404c-a405-39f80b9655f7" alt="8c116f87c7c38fee18bfa7669901f475.png" width="655" height="153">
3.  Once the response loads, grab the **JWT Token** located in the `Authorization: Bearer` header.
    - <img src="https://github.com/user-attachments/assets/3bc6cf1c-6567-4052-8390-c0d964bd4672" alt="e562b5a4f701cbac39d2a1c306da1ac7.png" width="641" height="230">

## Old vs New Query Format

This tool converts the custom queries from **Legacy BloodHound** to the **BloodHound CE** JSON format automatically. Here’s an example of what that looks like:

### Legacy BloodHound Format:

```json
{
    "queries": [
        {
            "name": "Query Name",
            "category": "Category",
            "queryList": [
                { 
                "final": true, 
                "query": "MATCH (n) RETURN n" 
                }
            ]
        }
    ]
}
```

### BloodHound CE Format:

```json
[
    {
        "name": "Query Name",
        "category": "Category",
        "query": "MATCH (n) RETURN n"
    }
]
```

You no longer need to handle this manually! Just use the tool, and it will handle the conversion for you.

## Support & Contribution

Enjoying my content? Show your support by sharing or starring my repositories!  
You can also support me on buy me a ko-fi to fuel more awesome content:

[![Buy me a KO-FI](https://img.shields.io/badge/-Buy%20me%20a%20KOFI-FF5F1D?style=for-the-badge&logo=KO-FI&logoColor=fff)](https://ko-fi.com/wafflesexploits)

💬 Have feedback or ideas? I’d love to hear your thoughts or suggestions!

**Looking for a Pentester? I’m open for contracts and full-time opportunities – feel free to DM me!**

## Credits

- [Make Bloodhound Cool Again: Migrating Custom Queries from Legacy BloodHound to BloodHound CE](https://medium.com/seercurity-spotlight/make-bloodhound-cool-again-migrating-custom-queries-from-legacy-bloodhound-to-bloodhound-ce-83cffcfe5b64)
    - His bash scripts helped me getting started!

Tool developed with ❤️ by **WafflesExploits**.

## License

This project is under the [Apache License 2.0](https://github.com/WafflesExploits/Bloodhound-query-legacy2ce/blob/main/LICENSE).
