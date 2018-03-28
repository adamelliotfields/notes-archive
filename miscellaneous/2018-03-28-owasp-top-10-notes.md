# OWASP Top 10 Notes
> :calendar: *March 28, 2018*

OWASP stands for Open Web Application Security Project - a non-profit organization for promoting web
application security.

The Top 10 is a list of common web application security vulnerabilities. The first version was
released in 2003; the latest version is 2017 RC2.

### #1. Injection

In an injection attack, a user can "inject" a command when entering data.

See the [Injection Prevention Cheat Sheet](https://www.owasp.org/index.php/Injection_Prevention_Cheat_Sheet).

### #2. Broken Authentication

One of the easiest ways to hack a user's account is to convince them to give you their password
(social engineering).

Broken application logic is also responsible for compromised accounts. For example, hackers can
abuse a faulty "Forgot my password" feature.

"Credential Stuffing" is when a hacker uses an automated program to attempt to log in as a user
using passwords obtained from a recent data breach.

Brute-force attacks are when a hacker simply tries every possible combination of characters to guess
a user's password.

See the [Authentication Cheat Sheet](https://www.owasp.org/index.php/Authentication_Cheat_Sheet).

### #3. Sensitive Data Exposure

The first thing to do is decide what data you need to be storing in the first place. If you're not
storing data, it can't be stolen.

For sensitive data that must be stored, encryption must be used properly. This means the encryption
key must be stored properly as well.

See the [Cryptographic Storage Cheat Sheet](https://www.owasp.org/index.php/Cryptographic_Storage_Cheat_Sheet).

### #4. XML eXternal Entities

XXE attacks are a subset of injection attacks. This attack specifically targets applications that
parse XML input.

See the [XXE Prevention Cheat Sheet](https://www.owasp.org/index.php/XML_External_Entity_%28XXE%29_Prevention_Cheat_Sheet).

### #5. Broken Access Control

An "Insecure Direct Object Reference" is a direct reference to a resource that is not being
validated. For example, if you can simply edit a URL to give you access to a section of the app that
you shouldn't have access to, then your access control is broken.

"Missing Function-level Access Control" is when any authenticated user can access administrative
sections of the app, despite not having administrator role-based access.

See the [Broken Access Control Cheat Sheet](https://www.owasp.org/index.php/Access_Control_Cheat_Sheet).

### #6. Misconfiguration

"Least Privelege" is a fundamental security principle, in which access to a particular resource,
function, or data should always be limited only to those who need. In other words, access to
everything should be shut off by default. Users can request upgraded priveleges if necessary.

Misconfigured error handling can also give a hacker information about the internals of your
application that can assist them with an attack. In other words, in production, you shouldn't have
(or need to have) any `console.warn` or `console.error` statements in your code.

Default passwords that never get changed are another way for hackers to access your application. For
example, if you're incorporating some 3rd-party tool with a default password of `admin`, you should
probably change that password.

### #7. Cross Site Scripting

Cross Site Scripting (XSS) attacks involve a hacker entering a script into an input form (wrapped
in `<script>` tags) which then gets embedded in the page.

For example, if you have a blog that allows users to write comments, an attacker could write a
script as a comment and any visitor to the page would then have that script run in their browser.

Any user input needs to be sanitized before being sent to the server.

See the [XSS Prevention Cheat Sheet](https://www.owasp.org/index.php/XSS_%28Cross_Site_Scripting%29_Prevention_Cheat_Sheet).

### #8. Insecure Deserialization

This is a new addition to the OWASP Top 10 for 2017.

Serialization is the process of converting an object into a format that makes it easier to
transport. For example, converting a JavaScript object to JSON. Deserialization is the inverse -
converting the JSON data to an object.

See the [Deserialization Cheat Sheet](https://www.owasp.org/index.php/Deserialization_Cheat_Sheet).

### #9. Using Components with Known Vulnerabilities

Software depends on other software.

If using a 3rd-party dependency, you are responsible for keeping that dependency up to date. If a
vulnerability is made public, you are responsible for patching it.

### #10. Insufficient Logging and Monitoring

Application logs should include access control failures and input validation failures.

Monitoring tools should have the capability of alerting an operator.
