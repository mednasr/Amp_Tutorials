# Internationalization ⚡
#### Introduction
How to support hreflang and internationalization with AMP. Internationalization and localization of content is an important feature<br /> that websites often embrace to provide maximum reach for their content or services.<br />

For static websites, a common site structure technique for addressing this is known as 'hreflang'. Hreflang is a part of the meta <br />data of a website and is used to annotate a page such that crawlers can discover alternative translations of a particular article.<br /> Search engines such as Google recognise websites that use hreflang.
The hreflang notation is used with the link tag to refer to<br /> another document:<br />
```
<link rel="alternate" hreflang="fr" href="https://www.example.com/path/to/french.html" />
```

AMP documents can also use the hreflang notation to point crawlers towards other versions of themselves in other languages.<br />

However, it's important to correctly setup the hreflang relationships between AMP documents correctly. Especially when one<br /> considers the existing meta data relationships between Canonical documents and AMP documents. Below are two examples of <br />how websites might structure their hreflang relationships for Canonical and AMP documents across an article.<br />

#### Example 1: Canonical + AMP

A common site structure pattern is pairing non-AMP canonical documents with AMP documents. The following diagram illustrates<br /> how to provide translations for this structure:
<img src="https://nasrweb.com/images/Sketch.png"/>

In this diagram, there is an English canonical desktop document and a corresponding AMP document. As per the official AMP <br /> Project documentation for discovery and distribution the English AMP document must include a link tag to the canonical<br />  document. Similarly, the canonical document includes a corresponding link tag to the AMP document.<br />

Additionally, this diagram includes French translations of both the canonical document and the AMP document. Therefore the<br />  documents must include link tags with hreflang attributes to connect the various alternative language versions of the canonical<br />  and AMP documents. The following rules apply:<br />

* Every canonical document must have a link tag with rel=amphtml pointing to its matching AMP document in the same language.
* Every AMP document must have a link tag with rel=canonical pointing to its matching canonical desktop document, again, in the same language.
* Every canonical document must have a link tag with rel=alternate and an hreflang attribute for each alternative language version of the canonical document.
* Every AMP document must have a link tag with rel=alternate and an hreflang attribute for each alternative language version of the AMP document.<br /><br />
Therefore, given an article with X language versions of itself (including English) each canonical document would include:<br /><br />
* 1 link tag with rel=amphtml
* And X link tags with rel=alternate and the hreflang attribute

#### Example 2: Canonical + Alternate + AMP
The next example is an expanded version of the first example. This example includes 3 versions of any given document in a given<br />language:<br />

* A canonical desktop document
* An alternate mobile site document
* An AMP document<br /><br />
The following diagram illustrates how to provide translations for this structure:

<img src="https://nasrweb.com/images/Sketch1.png"/>

The same rules from the previous example apply in this example with the addition of the following rules:<br />

* Every canonical document must have a link tag with rel=alternate and no hreflang attribute pointing to its matching alternate mobile document in the same language.
* Every alternate mobile document must have a link tag with rel=canonical pointing to its matching canonical desktop document, again, in the same language.
* Every alternate mobile document must have a link tag with rel=alternate and an hreflang attribute for each alternative language version of the alternate mobile document.

## License

AMP HTML is licensed under the [Apache License, Version 2.0](LICENSE).
