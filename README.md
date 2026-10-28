# California Culinary MCP Server 🍷🍽️

A **Model Context Protocol (MCP)** server built with **FastMCP** that exposes California restaurant data, structured reviews, and culinary maps to AI agents and clients through standardized resources and tools.

This repository serves as the data retrieval layer for culinary recommendation agents, enabling structured searches, semantic vibe matching, and review retrieval over STDIO transport.

## 📸 Demo & Verification

**Example JSON Response:**

```json
{
  "status": "found",
  "count": 1,
  "results": [
    {
      "name": "Iron Chef Kitchen",
      "neighborhood": "Downtown SF",
      "cuisine": "Japanese Fusion",
      "rating": 4.8,
      "price_range": "$$$",
      "signature_dish": "Omakase Tasting Menu",
      "vibes": [
        "moody",
        "upscale",
        "intimate"
      ],
      "description": "An intimate, dark-timbered culinary sanctuary..."
    }
  ]
}
```

## 🌟 Key Features

* **MCP Resource (`culinary-map://california`):** Exposes raw, unstructured text data covering 100+ California dining spots, vibes, and culinary contexts.
* **Structured Restaurant Search (`get_restaurant_info`):** Looks up restaurants by full or partial name and retrieves details such as ratings, price ranges, and signature dishes.
* **Semantic Vibe Matching (`recommend_by_vibe`):** Uses a two-pass search across structured vibe tags and raw text descriptions to match atmospheric keywords such as *moody*, *sun-drenched*, and *romantic*.
* **Review Retrieval (`get_review`):** Fetches detailed user reviews, visit dates, ratings, reviewer information, and image descriptions for specific dining locations.

## 🛠️ Project Structure

```text
├── server.py                          # Core FastMCP server and tool registrations
├── test.py                            # Client test script using MCP ClientSession
├── California-Culinary-Map.txt        # Unstructured culinary dataset
├── structured-restaurant-data.json    # Structured JSON restaurant database
├── augmented-user-review.json         # Augmented user review dataset
├── requirements.txt                   # Project dependencies
└── README.md                           # Project documentation
```

## 🚀 Getting Started

### 1. Prerequisites & Installation

Ensure you have **Python 3.10 or later** installed.

**Clone the repository:**

```bash
git clone https://github.com/aiwithnaveedd/Build-an-MCP-Server.git
cd california-culinary-mcp-server
```

**Create and activate a virtual environment:**

```bash
python -m venv .venv
```

On macOS/Linux:

```bash
source .venv/bin/activate
```

On Windows (PowerShell):

```powershell
.venv\Scripts\Activate.ps1
```

**Install dependencies:**

```bash
pip install fastmcp==3.1.0 mcp
```

### 2. Download Data Files

If the dataset files are not already included in the repository, download them using the following commands:

```bash
curl -O https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/_nbA_KMj1n7yBrpfz8rYkg/California-Culinary-Map.txt

curl -O https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/lxfhTQUrDCCD_JSMmr92VA/structured-restaurant-data.json

curl -O https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/oMqDIzTBNFT7KKJ0GW4-Cw/augmented-user-review.json
```

Ensure all three files are available in the project directory before running the server.

## 🧪 Testing the Server

Run the asynchronous MCP client test to verify the server connection over STDIO transport:

```bash
python test.py
```

The test client uses the standard MCP `ClientSession` to communicate with the server and verify its functionality.

## 🔌 MCP Tools & Resources API

### Resources

| Resource URI                | Description                                                                       |
| --------------------------- | --------------------------------------------------------------------------------- |
| `culinary-map://california` | Provides the complete raw-text map of California restaurants and culinary guides. |

### Tools

| Tool Name             | Parameters             | Description                                                                                         |
| --------------------- | ---------------------- | --------------------------------------------------------------------------------------------------- |
| `get_restaurant_info` | `restaurant_name: str` | Performs a partial-match search across the structured restaurant JSON dataset.                      |
| `recommend_by_vibe`   | `vibe: str`            | Searches structured vibe tags and raw-text paragraphs to recommend restaurants based on atmosphere. |
| `get_review`          | `restaurant_name: str` | Retrieves restaurant reviews, reviewer details, visit dates, ratings, and image context.            |

## 🧠 How It Works

1. **Data Access:** The server loads restaurant information from structured JSON files and unstructured culinary text.
2. **Restaurant Search:** The `get_restaurant_info` tool searches the structured dataset using full or partial restaurant names.
3. **Vibe-Based Recommendations:** The `recommend_by_vibe` tool searches structured vibe tags first, then checks raw-text descriptions for additional matches.
4. **Review Retrieval:** The `get_review` tool retrieves review information associated with a specified restaurant.
5. **MCP Communication:** AI clients connect to the server over STDIO and access its registered tools and resources through the Model Context Protocol.

## 📦 Dependencies

* **Python 3.10+**
* **FastMCP 3.1.0**
* **MCP Python SDK**

## 📜 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.
