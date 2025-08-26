# index.html
Crypto_dashboard_declare_html
# 📱 Phone Number Lookup Tool
# Requires: pip install phonenumbers

import phonenumbers
from phonenumbers import geocoder, carrier, timezone

def lookup_number(number: str):
    try:
        # Parse number (must include +country_code, e.g. +14155552671)
        parsed = phonenumbers.parse(number, None)
        
        # Collect details
        return {
            "Valid": phonenumbers.is_valid_number(parsed),
            "Country/Region": geocoder.description_for_number(parsed, "en"),
            "Carrier": carrier.name_for_number(parsed, "en"),
            "Timezones": timezone.time_zones_for_number(parsed)
        }
    except Exception as e:
        return {"Error": str(e)}

if __name__ == "__main__":
    print("📱 Phone Number Lookup Tool")
    print("Enter a number with country code (example: +14155552671)")
    while True:
        number = input("\nEnter phone number (or type 'exit' to quit): ")
        if number.lower() == "exit":
            break
        result = lookup_number(number)
        for key, value in result.items():
            print(f"{key}: {value}")
