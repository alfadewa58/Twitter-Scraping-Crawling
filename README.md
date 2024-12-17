# Twitter Data Scraper using Tweet-Harvest

This project allows users to crawl Twitter/X data using the **Tweet-Harvest** tool and process the collected tweets using Python. The script extracts tweet data for a specified keyword, saving it to a CSV file for further analysis.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Obtaining the Twitter Auth Token](#obtaining-the-twitter-auth-token)
- [Crawling Twitter Data](#crawling-twitter-data)
- [Processing and Displaying Data](#processing-and-displaying-data)
- [Output Example](#output-example)
- [Notes](#notes)

---

## Prerequisites

- **Python 3.7+**  
- **Node.js (v20+)**  
- **Chromium Browser**  
- **Twitter/X Account Login**  

### Required Packages:
- pandas  
- Node.js tools for Tweet-Harvest  

---

## Setup

### 1. Install Node.js and Required Packages
Run the following commands to install Node.js and `pandas`:

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
NODE_MAJOR=20
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list > /dev/null
sudo apt-get update
sudo apt-get install -y nodejs
pip install pandas
```

---

## Obtaining the Twitter Auth Token

The **Twitter Auth Token** is extracted from the cookies in your browser session when you log into your Twitter/X account:

1. **Log into your Twitter/X account** in a browser.  
2. **Open Developer Tools** (F12 or Ctrl+Shift+I in most browsers).  
3. Go to the **Application** or **Storage** tab and locate **Cookies**.  
4. Find the **auth_token** key and copy its value.  
5. Replace `'yourauthtoken'` in the script with this value:
   ```python
   twitter_auth_token = 'yourauthtoken'
   ```

---

## Crawling Twitter Data

1. **Set Search Parameters**: Modify the script as needed:
   ```python
   filename = 'kpr.csv'            # Output CSV filename
   search_keyword = 'kpr lang:id since:2024-12-01 until:2024-12-10'  
   # Search by date and language
   # Example: Remove "lang:" if you want only by date.
   limit = 100                     # Number of tweets to fetch
   twitter_auth_token = 'yourauthtoken'
   ```

2. **Run the Script**:
   Use the following command to start scraping:
   ```bash
   npx -y tweet-harvest@2.6.1 -o "{filename}" -s "{search_keyword}" -tab "LATEST" -l {limit} --token {twitter_auth_token}
   ```

3. **Output**:
   - Tweets are saved to: `/content/tweets-data/kpr.csv`  
   - Example: **116 tweets saved**

---

## Processing and Displaying Data

1. **Read the CSV File**:
   ```python
   import pandas as pd

   file_path = "tweets-data/{filename}"
   df = pd.read_csv(file_path, delimiter=",")
   display(df)
   ```

2. **Check Total Tweets**:
   ```python
   num_tweets = len(df)
   print(f"Jumlah tweet dalam dataframe adalah {num_tweets}.")
   ```

---

## Output Example

| conversation_id_str | created_at       | favorite_count | full_text                        | id_str            |
|----------------------|------------------|----------------|---------------------------------|------------------|
| 1868551637410746669 | Mon Dec 16 07:00 | 0              | HUT Ke-129 BRI ...              | 1868551637410746669 |
| 1868518844819759442 | Mon Dec 16 06:41 | 0              | @AdeptusAstartia Sepakat...     | 1868518844819759442 |

---

## Notes

1. **Auth Token**: Keep your `auth_token` private and do not share it.  
2. **Search by Date and Language**:  
   - To search tweets **by date and language**, use:  
     `search_keyword = 'yourkeyword lang:id since:YYYY-MM-DD until:YYYY-MM-DD'`.  
   - To search tweets **only by date**, remove `lang:id`.  
3. **Rate Limit**: Although you can crawl up to **2000 tweets**, it is recommended to limit scraping to **500 tweets per day** to avoid IP bans or account restrictions.  
4. **Session Validity**: The `auth_token` expires periodically. Refresh it by logging into Twitter/X and re-extracting it from cookies.  
---

## Disclaimer

This script is for **educational purposes only**. Use it responsibly and comply with Twitter/X's Developer Terms of Service.

---

### Research by Helmi Satria  
**Date**: March 30, 2024  
