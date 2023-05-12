The "泛微e-cology" system is a popular enterprise software developed by 泛微软件. Unfortunately, this system is vulnerable to XML entity injection attacks, particularly in the "/rest/ofs/RequestInfoByXml" path, which is used to submit XML requests to retrieve data from the system.

XML entity injection is a type of attack that takes advantage of the way XML parsers handle entities in the XML input. An entity is a reference to a piece of data, such as a string or a character, that is defined outside of the XML document and can be included in the document using an entity reference. If the XML parser is not properly configured, an attacker can use specially crafted entity references to inject malicious code into the XML input.

In the case of the "泛微e-cology" system, the vulnerability lies in the "/rest/ofs/RequestInfoByXml" path, which allows users to submit XML requests to retrieve data from the system. An attacker can craft a malicious XML request that includes an entity reference to a file on the system that they wish to retrieve, modify, or delete.

For example, an attacker can submit the following XML request, which contains an entity reference to the "weaver.properties" file in the "D:/WEAVER/ecology/WEB-INF/prop/" directory:

xml
Copy code
<?xml version="1.0" encoding="utf-8" ?>

<!DOCTYPE test[
<!ENTITY
bee SYSTEM "file:///D:/WEAVER/ecology/WEB-INF/prop/weaver.properties">
]>
<request>
  <data>&bee;</data>
</request>
When this request is submitted to the "/rest/ofs/RequestInfoByXml" path, the XML parser will replace the &bee; entity reference with the contents of the "weaver.properties" file. The attacker can then examine the XML response from the server to obtain sensitive information, such as passwords, usernames, and other configuration details.


This vulnerability can have serious consequences, as an attacker could potentially read, modify, or delete sensitive data from the system, resulting in a breach of confidentiality, integrity, and availability.

To mitigate this vulnerability, the 泛微软件 team should ensure that the XML parser is properly configured to prevent entity injection attacks. This can be achieved by disabling the resolution of external entities or by using a secure XML parser that is not vulnerable to these types of attacks.

In conclusion, the "泛微e-cology" system is vulnerable to XML entity injection attacks, particularly in the "/rest/ofs/RequestInfoByXml" path. The sample payload provided above can be used by attackers to retrieve sensitive information from the system. It is important for the 泛微软件 team to properly configure the XML parser to prevent these types of attacks and ensure the security of their system.
