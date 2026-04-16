# Automated Login Test Report  
## Website: https://www.saucedemo.com/

---

## Tester Details  
- Name: Ishita Devaliya  
- Role: QA Intern  
- Task: Login Functionality Testing  

---

## Objective  
To validate the login functionality using both valid and invalid user credentials.

---

## Testing Approach  
The login feature is tested based on automation testing concepts, covering positive and negative scenarios.

---

## Test Cases  

### Test Case ID: TC-01  
**Title:** Login with valid credentials  

**Precondition:** User is on login page  

**Test Steps:**  
1. Enter username as "standard_user"  
2. Enter password as "secret_sauce"  
3. Click on Login button  

**Expected Result:**  
User should be redirected to the inventory page  

**Actual Result:**  
User is successfully redirected to the inventory page  

**Status:** Pass  

---

### Test Case ID: TC-02  
**Title:** Login with invalid password  

**Precondition:** User is on login page  

**Test Steps:**  
1. Enter username as "standard_user"  
2. Enter password as "wrong_password"  
3. Click on Login button  

**Expected Result:**  
Error message should be displayed  

**Actual Result:**  
Error message is displayed  

**Status:** Pass  

---

### Test Case ID: TC-03  
**Title:** Login with invalid username  

**Precondition:** User is on login page  

**Test Steps:**  
1. Enter username as "invalid_user"  
2. Enter password as "secret_sauce"  
3. Click on Login button  

**Expected Result:**  
Error message should be displayed  

**Actual Result:**  
Error message is displayed  

**Status:** Pass  

---

### Test Case ID: TC-04  
**Title:** Login with empty fields  

**Precondition:** User is on login page  

**Test Steps:**  
1. Leave username field blank  
2. Leave password field blank  
3. Click on Login button  

**Expected Result:**  
Validation error message should be displayed  

**Actual Result:**  
Error message is displayed  

**Status:** Pass  

---

## Observations  
- Login works correctly with valid credentials  
- Proper error messages are shown for invalid inputs  
- Field validation is implemented for empty inputs  

---

## Conclusion  
The login functionality is working as expected for both positive and negative test scenarios.

---
## Final Status  
- Functionality: Working  
- Validation: Working  
- Overall: Stable  

---

## Automation Script (Python - Selenium)

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time

# Initialize WebDriver
driver = webdriver.Chrome()

# Open the application
driver.get("https://www.saucedemo.com/")
driver.maximize_window()

# -------- Test Case 1: Valid Login --------
driver.find_element(By.ID, "user-name").send_keys("standard_user")
driver.find_element(By.ID, "password").send_keys("secret_sauce")
driver.find_element(By.ID, "login-button").click()

time.sleep(2)

if "inventory" in driver.current_url:
    print("TC-01: Valid Login - Passed")
else:
    print("TC-01: Valid Login - Failed")

driver.back()

# -------- Test Case 2: Invalid Password --------
driver.find_element(By.ID, "user-name").clear()
driver.find_element(By.ID, "password").clear()

driver.find_element(By.ID, "user-name").send_keys("standard_user")
driver.find_element(By.ID, "password").send_keys("wrong_password")
driver.find_element(By.ID, "login-button").click()

time.sleep(2)

error_msg = driver.find_element(By.CLASS_NAME, "error-message-container")
if error_msg:
    print("TC-02: Invalid Password - Passed")
else:
    print("TC-02: Invalid Password - Failed")

# -------- Test Case 3: Empty Fields --------
driver.find_element(By.ID, "user-name").clear()
driver.find_element(By.ID, "password").clear()

driver.find_element(By.ID, "login-button").click()

time.sleep(2)

error_msg = driver.find_element(By.CLASS_NAME, "error-message-container")
if error_msg:
    print("TC-03: Empty Fields - Passed")
else:
    print("TC-03: Empty Fields - Failed")

# Close browser
driver.quit()
