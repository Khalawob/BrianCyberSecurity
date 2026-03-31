---
layout: default
title: Week 5: Web Application Security
page_heading: Week 5: Web Application Security
---

[← Back to homepage](/)

This lab teaches how to setup a WordPress security assessment lab using Wpscan on a kali Linux virtual machine and a WordPress server virtual machine. WPScan is a security scanner specifically designed for WordPress which unlike general purpose vulnerability scanners such as Nessus or Nmap, is built specifically to enumerate WordPress installations, examine installed plugins and themes against its CVE database, and perform authentication attacks on specified targets. The main difference between WPscan and a general scanner is that a general scanner would identify that port 80 is open and Apache is running, but it would not identify that the Salon Booking System plugin version 10.9.3 has 26 vulnerabilities with actions on how to stop it. WPscan's API key integration connects live scans to a vulnerability database which is up to date and maintained by the security community [1].

Make a new user with the administrator role so that they can install plugins and themes. We are going to set a weak password found from the Wikipedia weak password list [4].

<figure class="report-figure">
  <img src="/week5-web-application-security/p003_Figure_1_-_Create_New_User_called_Brian_with_password_as_Admin.png" alt="Figure 1 - Create New User called Brian with password as Admin">
  <figcaption>Figure 1 - Create New User called Brian with password as Admin</figcaption>
</figure>

<figure class="report-figure">
  <img src="/week5-web-application-security/p004_Figure_2_-_Administartor_Role.png" alt="Figure 2 - Administartor Role">
  <figcaption>Figure 2 - Administartor Role</figcaption>
</figure>

Install vulnerable plugins and themes which are going to be scanned with WPscan.

<figure class="report-figure">
  <img src="/week5-web-application-security/003_Figure_4_-_Vulnerable_Theme_part1.png" alt="Figure 3 - Vulnerable Plugin [2]">
  <figcaption>Figure 3 - Vulnerable Plugin [2]</figcaption>
</figure>

<figure class="report-figure">
  <img src="/week5-web-application-security/p004_Figure_4_-_Vulnerable_Theme.jpeg" alt="Figure 4 - Vulnerable Theme">
  <figcaption>Figure 4 - Vulnerable Theme</figcaption>
</figure>

## 1: Vulnerability Database Update and Plugin Enumeration

Update WPscan Database

This is used so the Vulnerability database contains the latest information on vulnerabilities found in plugins

<figure class="report-figure">
  <img src="/week5-web-application-security/p005_Figure_5_-_WPscan_Updated.jpeg" alt="Figure 5 - WPscan Updated">
  <figcaption>Figure 5 - WPscan Updated</figcaption>
</figure>

Connect the WPscan API key to wpscan

This is used to access the database of vulnerabilities and check if there is any vulnerabilities in the plugins or themes

<figure class="report-figure">
  <img src="/week5-web-application-security/p005_Figure_6_-_API_Key.jpeg" alt="Figure 6 - API Key">
  <figcaption>Figure 6 - API Key</figcaption>
</figure>

WPScan WordPress URL enumerate -p

WPScan checks its database of vulnerabilities for the latest vulnerabilities and identifies plugins that have been installed.

<figure class="report-figure">
  <img src="/week5-web-application-security/p006_Figure_7_-_Output_Page_1.png" alt="Figure 7 - Output Page 1">
  <figcaption>Figure 7 - Output Page 1</figcaption>
</figure>

This image shows the plugin installed and the number of vulnerabilities identified along with fixes.

<figure class="report-figure">
  <img src="/week5-web-application-security/p007_Figure_8_-_Identified_Plugin_Vulnerabilities.jpeg" alt="Figure 8 - Identified Plugin Vulnerabilities">
  <figcaption>Figure 8 - Identified Plugin Vulnerabilities</figcaption>
</figure>

<figure class="report-figure">
  <img src="/week5-web-application-security/p007_Figure_9_-_Identified_Plugin_Vulnerabilities_page_2.jpeg" alt="Figure 9 - Identified Plugin Vulnerabilities page 2">
  <figcaption>Figure 9 - Identified Plugin Vulnerabilities page 2</figcaption>
</figure>

## 2: Full Scan for Plugins Themes and WordPress Version Detection

--Enumerate vp,vt,tt

The command in figure 10 performs a comprehensive scan that targets Vulnerable plugins using “VP”, Vulnerable Themes are targeted with “VT” while “TT” lists all the themes and attempts to find associated vulnerabilities.

<figure class="report-figure">
  <img src="/week5-web-application-security/p008_Figure_10_-_wpscan_--url_http192.168.123.65_--enumerate_vpvttt.png" alt="Figure 10 - wpscan --url http://192.168.123.65 --enumerate vp,vt,tt">
  <figcaption>Figure 10 - wpscan --url http://192.168.123.65 --enumerate vp,vt,tt</figcaption>
</figure>

The theme being used has been identified along with 1 vulnerability related to reflected cross site scripting

<figure class="report-figure">
  <img src="/week5-web-application-security/p009_Figure_11_-_wpscan_--url_http192.168.123.65_--enumerate_vpvttt_Identified_Theme_.png" alt="Figure 11 - wpscan --url http://192.168.123.65 --enumerate vp,vt,tt (Identified Theme and associated Vulnerabilities)">
  <figcaption>Figure 11 - wpscan --url http://192.168.123.65 --enumerate vp,vt,tt (Identified Theme and associated Vulnerabilities)</figcaption>
</figure>

This Image also contains the plugins in use along with 26 vulnerabilities such as reflected cross-site scripting and sensitive data disclosure.

<figure class="report-figure">
  <img src="/week5-web-application-security/p009_Figure_12_-_wpscan_--url_http192.168.123.65_--enumerate_vpvttt_Plugins_and_Vulne.png" alt="Figure 12 - wpscan --url http://192.168.123.65 --enumerate vp,vt,tt (Plugins and Vulnerabilities)">
  <figcaption>Figure 12 - wpscan --url http://192.168.123.65 --enumerate vp,vt,tt (Plugins and Vulnerabilities)</figcaption>
</figure>

More plugin Vulnerabilities

<figure class="report-figure">
  <img src="/week5-web-application-security/p010_Figure_14_-_WPscan_plugin_vulnerability_page_3.jpeg" alt="Figure 14 - WPscan plugin vulnerability page 3">
  <figcaption>Figure 14 - WPscan plugin vulnerability page 3</figcaption>
</figure>

This page contains the theme WordPress is using and the reflected cross site scripting vulnerability it found.

<figure class="report-figure">
  <img src="/week5-web-application-security/p010_Figure_15-_WPscan_theme_vulnerabilities.png" alt="Figure 15- WPscan theme vulnerabilities">
  <figcaption>Figure 15- WPscan theme vulnerabilities</figcaption>
</figure>

### WPScan Enumeration (VP, VT, AP, TT Scans) CIA Triad Impact

| Confidentiality - Breached | Integrity – Breached | Availability – High Risk |
| --- | --- | --- |
| The WPscan Enumeration reveals the usernames and the names and versions of the plugins and themes which give attackers a detailed guide of the targets system without any authentication | Knowing exact plugin versions allows an attacker to identify unpatched vulnerabilities such as SQL injection or privilege escalation, which could be used to modify database records or inject malicious content. | Certain vulnerabilities were identified like Cross-Site Request Forgery and unauthorised file upload, could be used to corrupt or delete site content and cause service disruption |

## BruteForcing Login Passwords

WPSCAN Brute force Login

The command in Figure 16 attempts to brute force login to a account called “Brian” on WordPress using the list of passwords contained in passwords.txt.

<figure class="report-figure">
  <img src="/week5-web-application-security/p011_Figure_16-_wpscan_--url_http192.168.123.65_--passwords_homekaliDesktoppasswords..jpeg" alt="Figure 16- wpscan --url http://192.168.123.65 --passwords /home/kali/Desktop/passwords.txt --usernames Brian">
  <figcaption>Figure 16- wpscan --url http://192.168.123.65 --passwords /home/kali/Desktop/passwords.txt --usernames Brian</figcaption>
</figure>

<figure class="report-figure">
  <img src="/week5-web-application-security/p012_Figure_17_-_Password_List_that_is_being_used.png" alt="Figure 17 - Password List that is being used">
  <figcaption>Figure 17 - Password List that is being used</figcaption>
</figure>

The output shows that a valid combination of credentials was found saying “Username: Brian” and “Password: admin”

<figure class="report-figure">
  <img src="/week5-web-application-security/p013_Figure_18-_Output_of_wpscan_--url_http192.168.123.65_--passwords_homekaliDesktop.png" alt="Figure 18- Output of &quot;wpscan --url http://192.168.123.65 --passwords /home/kali/Desktop/passwords.txt --usernames Brian&quot;">
  <figcaption>Figure 18- Output of "wpscan --url http://192.168.123.65 --passwords /home/kali/Desktop/passwords.txt --usernames Brian"</figcaption>
</figure>

### Brute Force Attack (Brian / admin) CIA Triad Impact

| Confidentiality - Breached | Integrity – Breached | Availability – High Risk |
| --- | --- | --- |
| Gaining valid administrator credentials exposes all user data, email addresses and any private content managed through the WordPress dashboard | An authenticated administrator can install malicious plugins, modify page content, or alter site settings and directly compromise the trustworthiness of all data | An attacker with administrator access could deactivate all plugins, delete posts, pages or corrupt the database |

## 4: Scanning with API Key for Detailed Vulnerabilities

Using a API key to find detailed vulnerabilities

The AP option enumerates all plugins and checks each one in the WPscan vulnerability database

<figure class="report-figure">
  <img src="/week5-web-application-security/p014_Figure_19_-_API_Token_Enumerate_AP.png" alt="Figure 19 - API Token Enumerate AP">
  <figcaption>Figure 19 - API Token Enumerate AP</figcaption>
</figure>

<figure class="report-figure">
  <img src="/week5-web-application-security/p015_Figure_18_-_WPScan_API-assisted_vulnerability_enumeration_output.png" alt="Figure 18 - WPScan API-assisted vulnerability enumeration output">
  <figcaption>Figure 18 - WPScan API-assisted vulnerability enumeration output</figcaption>
</figure>

Excluding specific scans and setting a delay

Excluding specific scans is used for focusing on components that are likely to have vulnerabilities such as plugins and themes due to them being updated often and increasing the risk of containing exploitable code. The benefits behind this is that it reduces scan time and reducing the impact of server resources and network traffic.

The throttle on the other hand creates a delay between each http request sent by the WPscan. This is used to avoid detection because the delay makes the scan appear seem more like regular user traffic and is less likely to get blocked. A benefit is that it reduces server strain

<figure class="report-figure">
  <img src="/week5-web-application-security/p016_Figure_20_-_Throttle_and_Excluding_Scan_Types.png" alt="Figure 20 - Throttle and Excluding Scan Types">
  <figcaption>Figure 20 - Throttle and Excluding Scan Types</figcaption>
</figure>

<figure class="report-figure">
  <img src="/week5-web-application-security/p016_Figure_21_-ThrottleDelay_Output_Themes.png" alt="Figure 21 - Throttle/Delay Output Themes">
  <figcaption>Figure 21 - Throttle/Delay Output Themes</figcaption>
</figure>

Figure 22 - Plugin Vulnerabilities

## Security Implications

The 26 plugin vulnerabilities and the Theme vulnerability that were found critically affect the security of the system as information about these vulnerabilities are on WPscan and guides on how to exploit them. These could be used to commit SQL injections to steal user data from the database and 1 of the vulnerabilities include a stored cross site scripting attack which users with administrator access could use to commit these attacks. The best way to solve this is to update the plugins and themes.

## Comparison Table between VP, VT, AP, TT

| VP | VT | AP | TT |
| --- | --- | --- | --- |
| Scans vulnerable Plugins only | Scans Vulnerable Themes only | Scans all plugins regardless of the presence of vulnerabilities | Scans all themes regardless of vulnerabilities |
| Much quicker than scanning all plugins | Much quicker than scanning all themes | Slower than scanning vulnerable plugins only | Slower than scanning vulnerable themes. |

---

[← Back to homepage](/)
