import pandas as pd
import requests
import json
# List of ZWL codes
zwl_codes = [
    "ZWL003370",
    "ZWL002088",
    "ZWL006702",
    "ZWL008776",
    "ZWL003918",
    "ZWL004079",
    "ZWL008309",
    "ZWL002433",
    "ZWL007390",
    "ZWL004767",
    "ZWL006016",
    "ZWL003283",
    "ZWL007311",
    "ZWL005919",
    "ZWL001822",
    "ZWL008208",
    "ZWL001362",
    "ZWL002162",
    "ZWL009712",
    "ZWL005963",
    "ZWL008297",
    "ZWL005424",
    "ZWL008585",
    "ZWL008599",
    "ZWL006535",
    "ZWL006545",
    "ZWL009719",
    "ZWL008890",
    "ZWL007119",
    "ZWL004747",
    "ZWL004802",
    "ZWL004665",
    "ZWL005999",
    "ZWL003360",
    "ZWL007187",
    "ZWL007344",
    "ZWL008438",
    "ZWL005494",
    "ZWL009519",
    "ZWL001687",
    "ZWL005569",
    "ZWL003027",
    "ZWL001337",
    "ZWL001579",
    "ZWL006699",
    "ZWL008512"
]
#
# change the locality in the loop
import requests

cookies = {
    'cid': 'bb687dd1-e9bc-413a-97c7-50ea6eea6856',
    'zat': '5afwl0Ruo2kLdbhbQry8HUHwjW6bxv7nGTLR048Wbgc.rboMSahPS3I5LDijwp65QUMuyqKzquSXuI7Ipq_Vi68',
    'ttaz': '1725540660',
    'ak_bmsc': '8E0BA6A75705446DE28E4528F0D6CC63~000000000000000000000000000000~YAAQXHxBFzn1HwmRAQAAiiAuKBh+ttd7ZQt/wxOf7tB9sM/mpqGUWjbDdBl5CiQInkYjSjOOieqiTs//u6cQ4QFwZwkxNuEYHeV09+91chaST1B0NhyFQmUunEnar2lqfNZ75i+VG3k/k/3lbKnktKJugwLfxfyojY8B5uTKODvGn54dCr5/x5uFUX7ntNHAu3vv4q78TX4L8VMoLEjfMsPX93M0veEhDE5XtzqE++VbetGLvP22ZkdjvqXQ1sgkCFJgkw4Of3m05ADo2uD9uwB0MpdbZLUhwPYDKNWtY6OqkwNhNf3DfyAdqZrusDtzLLN5Kca2GQAdBr+mEVPypY6QzRp37okjvUSnRbR5TZKkXeBUNp+rd/6gX3wAeFvlyo1vJKhJxbF9igz53Ygh3VY/yWKI1G0/WRVOiV4GzGeWoA==',
    'AKA_A2': 'A',
    '__Host-csrft': '42acf6f74e2397a94e5aa7efd1ac0eaf4495b71c62f4cbeef67e13faa5e07aa45445',
    'bm_sv': '59850D9C2AD06447D21FD7719D0A9669~YAAQXHxBFy3yNAmRAQAA5JZlKBh0vWS1KwtX++UuKwLwdmUtnWAkt+bBKYKrC0m25G60p4dk9Os+hfRh9U/kwOyWdU1SAm39XuHPLZFTpa4HZWeT3BdsMvXLhEbHEqW7Qsrv2ZZ6deTn1FAO5/Es0jPQmuwKrGps3Q4bgxLl1b1YMcSMrf47adSXBtH9rIqIeryel+rAsTxYR4gh2tzIupO2nDpRBzONMzQeg2x8SuootnVMTGUvAGyDuywAVDMBKSJAOZPaxg==~1',
}

headers = {
    'accept': 'application/json, text/plain, /',
    'accept-language': 'en-US,en;q=0.8',
    'api-key': '1dd7717aca479d95a05ddf0281511191',
    # 'cookie': 'cid=bb687dd1-e9bc-413a-97c7-50ea6eea6856; zat=5afwl0Ruo2kLdbhbQry8HUHwjW6bxv7nGTLR048Wbgc.rboMSahPS3I5LDijwp65QUMuyqKzquSXuI7Ipq_Vi68; ttaz=1725540660; ak_bmsc=8E0BA6A75705446DE28E4528F0D6CC63~000000000000000000000000000000~YAAQXHxBFzn1HwmRAQAAiiAuKBh+ttd7ZQt/wxOf7tB9sM/mpqGUWjbDdBl5CiQInkYjSjOOieqiTs//u6cQ4QFwZwkxNuEYHeV09+91chaST1B0NhyFQmUunEnar2lqfNZ75i+VG3k/k/3lbKnktKJugwLfxfyojY8B5uTKODvGn54dCr5/x5uFUX7ntNHAu3vv4q78TX4L8VMoLEjfMsPX93M0veEhDE5XtzqE++VbetGLvP22ZkdjvqXQ1sgkCFJgkw4Of3m05ADo2uD9uwB0MpdbZLUhwPYDKNWtY6OqkwNhNf3DfyAdqZrusDtzLLN5Kca2GQAdBr+mEVPypY6QzRp37okjvUSnRbR5TZKkXeBUNp+rd/6gX3wAeFvlyo1vJKhJxbF9igz53Ygh3VY/yWKI1G0/WRVOiV4GzGeWoA==; AKA_A2=A; __Host-csrft=42acf6f74e2397a94e5aa7efd1ac0eaf4495b71c62f4cbeef67e13faa5e07aa45445; bm_sv=59850D9C2AD06447D21FD7719D0A9669~YAAQXHxBFy3yNAmRAQAA5JZlKBh0vWS1KwtX++UuKwLwdmUtnWAkt+bBKYKrC0m25G60p4dk9Os+hfRh9U/kwOyWdU1SAm39XuHPLZFTpa4HZWeT3BdsMvXLhEbHEqW7Qsrv2ZZ6deTn1FAO5/Es0jPQmuwKrGps3Q4bgxLl1b1YMcSMrf47adSXBtH9rIqIeryel+rAsTxYR4gh2tzIupO2nDpRBzONMzQeg2x8SuootnVMTGUvAGyDuywAVDMBKSJAOZPaxg==~1',
    'priority': 'u=1, i',
    'referer': 'https://www.weatherunion.com/',
    'sec-ch-ua': '"Not)A;Brand";v="99", "Brave";v="127", "Chromium";v="127"',
    'sec-ch-ua-mobile': '?1',
    'sec-ch-ua-platform': '"Android"',
    'sec-fetch-dest': 'empty',
    'sec-fetch-mode': 'cors',
    'sec-fetch-site': 'same-origin',
    'sec-gpc': '1',
    'user-agent': 'Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Mobile Safari/537.36',
}

# Loop through ZWL
for zwl_code in zwl_codes:
    params = {
        'city_id': 'ZWC000136',
        'locality_id': zwl_code,
        'duration_day': '180',
    }

    response = requests.get(
        'https://www.weatherunion.com/gw/weather/external/v0/download_previous_data',
        params=params,
        cookies=cookies,
        headers=headers,
    )

    # Parse the response JSON
    try:
        y = response.json()
        # Extract and print the "link" field
        print(f"Link for {zwl_code}: {y.get('link', 'No link found')}")
    except json.JSONDecodeError:
        print(f"Response for {zwl_code} is not valid JSON.")

  
