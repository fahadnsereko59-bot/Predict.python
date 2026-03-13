import random
import time

# ... (Keep your existing Predict class and scraping functions) ...

def run_predictor():
    engine = Predict()
    print("--- predict: BetPawa Virtual AI Started ---")
    
    with sync_playwright() as p:
        # Launch with a real user agent to blend in
        browser = p.chromium.launch(headless=True)
        context = browser.new_context(
            user_agent="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36"
        )
        page = context.new_page()
        
        try:
            while True:
                # 1. Random delay before starting (2-5 seconds)
                time.sleep(random.uniform(2, 5)) 
                
                print("\n[Scanning] Fetching live data...")
                page.goto("https://www.betpawa.ug")
                page.wait_for_selector(".game-row", timeout=15000)
                
                # ... (Your prediction logic here) ...
                
                # 2. Adjusted frequency for Render
                # Virtual rounds usually happen every 4-5 minutes.
                # We wait 4 minutes + a random offset (10-40 seconds)
                wait_time = 240 + random.randint(10, 40)
                print(f"Waiting {wait_time} seconds for next round...")
                time.sleep(wait_time)
                
        except Exception as e:
            print(f"Connection issue: {e}. Retrying in 60s...")
            time.sleep(60)
        finally:
            browser.close()
