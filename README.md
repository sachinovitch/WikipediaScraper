# import the requests library
import requests

# assign the root url (without /status) to the root_url variable for ease of reference
root_url = 'https://country-leaders.onrender.com'

# assign the /status endpoint to another variable called status_url
status_url = root_url + '/status'

# query the /status endpoint using the get() method and store it in the req variable
req = requests.get(status_url)

# check the status_code using a condition and print appropriate messages
if req.status_code == 200:
    print(req.text)
else:
    print('Error:', req.status_code)


# Set the countries_url variable
countries_url = root_url + '/countries'

# query the /countries endpoint using the get() method and store it in the req variable
req = requests.get(countries_url)

# Get the JSON content and store it in the countries variable
countries = req.json()

# display the request's status code and the countries variable
print('Status Code:', req.status_code)
print('Countries:', countries)


# Set the cookie_url variable
cookie_url = "https://country-leaders.onrender.com/cookie"

# Query the endpoint, set the cookies variable and display it
cookies = requests.get(cookie_url).cookies
print("Cookies:", cookies)

# Query the /countries endpoint, assign the output to the countries variable
countries_url = "https://country-leaders.onrender.com/countries"
countries = requests.get(countries_url, cookies=cookies).json()

# Display the countries variable
print("Countries:", countries)


# Set the leaders_url variable
leaders_url = "https://country-leaders.onrender.com/leaders"

# Query the /leaders endpoint, assign the output to the leaders variable
leaders = requests.get(leaders_url).json()

# Display the leaders variable
print("Leaders:", leaders)

# Query the /leaders endpoint using cookies and parameters (take any country in countries)
# Assign the output to the leaders variable
country = "your_country_name_here"
leaders = requests.get(leaders_url, cookies=cookies, params={"country": country}).json()

# Display the leaders variable
print("Leaders for", country, ":", leaders)


def get_leaders():
    # Define the urls
    leaders_url = "https://country-leaders.onrender.com/leaders"
    countries_url = "https://country-leaders.onrender.com/countries"

    # Get the cookies
    cookie_url = "https://country-leaders.onrender.com/cookie"
    cookies = requests.get(cookie_url).cookies

    # Get the countries
    countries = requests.get(countries_url, cookies=cookies).json()

    # Loop over the countries and save their leaders in a dictionary
    leaders_per_country = {}
    for country in countries:
        leaders = requests.get(leaders_url, cookies=cookies, params={"country": country}).json()
        leaders_per_country[country] = leaders

    # Return the dictionary
    return leaders_per_country

# Test the function and save the result in the leaders_per_country dictionary
leaders_per_country = get_leaders()

# Check the output
print("Leaders per country:", leaders_per_country)