# dashboard.py

import streamlit as st
import requests

API_URL = "http://127.0.0.1:8000"

st.title('AI Domain Trading Sandbox')

# Display domains
response = requests.get(f"{API_URL}/domains/")
if response.status_code == 200:
    domains = response.json()['domains']
    st.subheader("Discovered Domains")
    for domain in domains:
        st.write(f"Domain: {domain[1]}, Valuation: {domain[2]}, Target Sell Price: {domain[4]}")

# Simulate domain purchase
st.subheader("Buy Domain")
domain_name = st.text_input("Domain Name")
valuation_score = st.number_input("Valuation Score", min_value=0.0, max_value=1.0, value=0.5)
acquired_price = st.number_input("Acquired Price", min_value=0.0, value=100.0)
target_sell_price = st.number_input("Target Sell Price", min_value=0.0, value=1500.0)

if st.button("Buy Domain"):
    response = requests.post(f"{API_URL}/buy/", json={
        "name": domain_name,
        "valuation_score": valuation_score,
        "acquired_price": acquired_price,
        "target_sell_price": target_sell_price
    })
    if response.status_code == 200:
        st.success(response.json()['message'])
    else:
        st.error("Error purchasing domain.")

# Simulate domain sale
st.subheader("Sell Domain")
domain_id = st.number_input("Domain ID to Sell", min_value=1)
if st.button("Sell Domain"):
    response = requests.post(f"{API_URL}/sell/", json={"domain_id": domain_id})
    if response.status_code == 200:
        st.success(response.json()['message'])
    else:
        st.error("Error selling domain.")