import random
import time
from selenium import webdriver
from selenium.webdriver.edge.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Configuration
edge_driver_path = "C:\\WebDriver\\msedgedriver.exe"  # Path to Edge WebDriver
google_form_url = "https://docs.google.com/forms/d/e/1FAIpQLSctXZ_4bwzYi8RKMVD0otlOrzYHIyGuyT-70Cjxvw5ygU3v5w/viewform"
repeat_count = 5  # Number of times to submit the form

# Initialize Edge WebDriver
service = Service(edge_driver_path)
driver = webdriver.Edge(service=service)
wait = WebDriverWait(driver, 10)

for attempt in range(repeat_count):
    print(f"🔄 Attempt {attempt + 1} of {repeat_count}")

    # Open Google Form
    driver.get(google_form_url)

    # Wait for the page to load
    question_blocks = wait.until(EC.presence_of_all_elements_located((By.CLASS_NAME, "Qr7Oae")))

    # Flag to ensure "3" is clicked only once
    rating_three_selected = False

    for question in question_blocks:
        rating_options = question.find_elements(By.CLASS_NAME, "Od2TWd")  # Find rating buttons in each block
        if rating_options:
            # If we haven't selected "3" yet, pick it randomly from a question
            if not rating_three_selected and random.random() < 1 / len(question_blocks):
                rating_options[2].click()  # Select 3 (index 2)
                rating_three_selected = True
            else:
                # Pick between 4-5 ratings
                random.choice(rating_options[3:5]).click()  # Select 4 or 5

    # ---- Submit Form ----
    try:
        submit_button = wait.until(EC.element_to_be_clickable((By.XPATH, "//span[text()='Submit' or text()='ส่ง']")))
        driver.execute_script("arguments[0].scrollIntoView(true);", submit_button)
        time.sleep(2)
        submit_button.click()
        print(f"✅ Submission {attempt + 1} completed.")

    except Exception as e:
        print(f"❌ Error on attempt {attempt + 1}: {e}")
    
    # Wait before next attempt
    time.sleep(3)

print("🎉 All form submissions completed!")
driver.quit()
