# Splunk-Project

This project leverages Splunk to analyze and visualize login data. The dataset includes login timestamps, user IDs, IP addresses, and device details.

Prerequisites Before you begin, ensure you have the following installed:

Splunk: Download and Install Splunk Dataset: https://www.kaggle.com/datasets/dasgroup/rba-dataset

[Optional] Replace the sample data with your dataset.

Usage Start Splunk and make sure it's running.

Upload the sample data or your dataset into Splunk.

Execute the provided queries in Splunk to analyze and visualize the login data.

Queries

1. Identify Countries with Account Takeover
index="final_6_splunkproject" "Is Account Takeover"="TRUE" | stats count by Country | sort - count

2. Details of Account Takeover Incidents
index="final_6_splunkproject" | search "Is Account Takeover"="TRUE" | table "User ID", "Is Account Takeover", Country, "Device Type"

3. Top 10 Attack IPs
index="final_6_splunkproject" | search "Is Attack IP"="TRUE" | stats count by "IP Address" | sort - count | head 10

4. Account Takeover and Attack IP Analysis
index="final_6_splunkproject" | search "Is Attack IP"="TRUE" "Is Account Takeover"="TRUE" | stats count by "IP Address", "Is Account Takeover" | table "IP Address", "Is Account Takeover", count | head 10

5. Login Status and Attack IP Statistics
index=final_6_splunkproject "Is Attack IP"="TRUE" | stats count by "Login Successful", "Is Attack IP"

6. Top 10 Browsers Involved in Attack IP
index=final_6_splunkproject "Is Attack IP"="TRUE" | top limit=10 "Browser Name and Version"

7. Top 10 Countries with Attack IP
index=final_6_splunkproject "Is Attack IP"="TRUE" | top limit=10 Country

8. Top 10 User Agent Strings in Attack IP
index=final_6_splunkproject "Is Attack IP"="TRUE" | top limit=10 "User Agent String"

9. Statistics on Account Takeover Incidents
index=final_6_splunkproject "Is Attack IP"="TRUE" | stats count by "Is Account Takeover"

10. Find users with multiple failed login attempts
index=final_6_splunkproject "Login Successful"="FALSE" | stats count by "User ID" | where count > 3 | table "User ID", count | sort - count | head 10
