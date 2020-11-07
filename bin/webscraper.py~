import requests # for requesting the URL
from lxml import etree, html # to parse HTML
import pandas as pd # data frame
import time # to pause the browser when necessary.

# Firefox browser
from selenium import webdriver
from selenium.webdriver.support.ui import Select
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.common.by import By
from selenium.webdriver.support import expected_conditions as EC

# Parameters configuration
URL = "https://www.28hse.com/en/"
OUTPUT_FILENAME = "aprt_data.csv"

# Scraping class
class Scraper():
    __sales_price = []
    __floor = []
    __room = []
    __net_floor_sqft = []
    __property_age = []
    __address = []
    __district = []
    __number_of_rows = 0

    def __init__(self, URL, OUTPUT_FILENAME):
        self.url = URL
        self.output_filename = OUTPUT_FILENAME

        print("Loading Firefox..") # Alerting
        self.driver = webdriver.Firefox(executable_path=r"../drivers/geckodriver")

        print("Loaded.") # Alerting

    def get_to_page(self):
        self.driver.get(self.url) # Go to the page.
        self.driver.find_element(By.CLASS_NAME, 'maintagbutton').click() # Clicks the search button.
        self.driver.find_element(By.XPATH, '/html/body/div[3]/div[2]/div/h4/p/a[1]').click() # Clicks the sales link.
       
        # Finding the total number of rows
        res = self.driver.page_source
        content = html.fromstring(res)
        __number_of_rows = content.xpath('/html/body/div[2]/form/div[3]/div[1]/div[4]/div[1]/div/em')[0].text        
        print("Total rows:" + __number_of_rows)

        # Finding the container that contains the rows
        rows = self.driver.find_element(By.CLASS_NAME, 'agentad_outer')

        # Looping over each row in the list
        for r in rows:
            r.click()

        #print(res)

        time.sleep(5)
        
        self.driver.close()

print("Starting program..")
scraper = Scraper(URL, OUTPUT_FILENAME)
scraper.get_to_page()



        

