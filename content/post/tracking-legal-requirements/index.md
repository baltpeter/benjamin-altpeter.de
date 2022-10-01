---
title: "Legal requirements for tracking and consent dialogs under the GDPR and ePrivacy directive"
slug: "tracking-legal-requirements"
date: 2022-09-20T16:54:38+02:00
description: "Tracking and consent dialogs have become ubiquitous with seemingly every website and app pleading users to agree to their personal data being processed and their behaviour being tracked, often with the help of tens or even hundreds of third-party companies. But the bar for legally performing tracking in the EU is high. In this post, I detail both the legal requirements for tracking and collecting consent in general and present a comprehensive list of criteria for a legally compliant consent dialog."
tags: ["cookie banner", "consent notice", "legal criteria", "gdpr", "eprivacy directive"]
featured_image: "/tracking-legal-requirements/consent-dialogs.png"
---

Consent and cookie notices seem ubiquitous both on the web and on mobile. They are an effort by publishers to comply with data protection legislation like the *General Data Protection Regulation* (GDPR), an EU regulation that went into force in 2018 and mandates strict legal guidelines for processing personal data. The flood of consent dialogs is often wrongly attributed as a shortcoming of the GDPR, when in fact the GDPR and other applicable data protection legislation provide strong consumer protections and set a high bar for what an acceptable way of collecting consent is, that many consent dialogs fail to meet. The ubiquity of consent dialogs is a manifestation of the common belief that consent is the only possible legal basis under the GDPR, which is not true unless data is used for tracking, as well as of companies deliberately violating the law, e.g. by making use of nudging and dark patterns meant to coerce the user into giving consent and discouraging them from opting out.

The danger of such dark patterns and nudging [is](https://fil.forbrukerradet.no/wp-content/uploads/2018/06/2018-06-27-deceived-by-design-final.pdf) [well](https://jdsr.se/ojs/index.php/jdsr/article/view/54/31) [established](https://hal.inria.fr/hal-03117307/document). Recently, in a joint decision with other EU data protection authorities, the Belgian authority [ruled](https://www.gegevensbeschermingsautoriteit.be/publications/beslissing-ten-gronde-nr.-21-2022-english.pdf) that the IAB *Transparency & Consent Framework*, an industry standard for collecting user consent and communicating consent status information to advertising and tracking scripts that is used on a majority of websites, [violates the GDPR and is not able to acquire valid consent](https://www.iccl.ie/news/gdpr-enforcer-rules-that-iab-europes-consent-popups-are-unlawful/).

In this post, we'll have a detailed look at both the [legal requirements for tracking in general](#legal-background), as well as the [specific requirements for legally obtaining consent for tracking](#criteria-for-compliant-consent-dialogs). I also present a [comprehensive list of criteria for a legally compliant consent dialog](#list-of-criteria) based on the GDPR, DPA recommendations, and court rulings.

## Legal Background

We'll start by looking at which laws are relevant for tracking and under which conditions data collection and processing are lawful or unlawful.

### Processing of Personal Data

The primary law for data protection in the EU is the *General Data Protection Regulation* (GDPR), which went into force in 2018 and mandates a data protection framework that is consistent across the whole EU and also more strict than previous laws in this area. As an EU regulation, it is applicable law in all EU member states without them needing to tranpose it into their national laws.

The GDPR deals with the *processing* of *personal data* (Art. 2(1) GDPR). These legal terms are defined in Art. 4 GDPR:

> (1) ‘personal data’ means any information relating to an identified or identifiable natural person […]; [i.e.] one who can be identified, directly or indirectly, in particular by reference to an identifier such as a name, an identification number, location data, an online identifier or […] the physical, physiological, genetic, mental, economic, cultural or social identity […]

> (2) ‘processing’ means any operation […] performed on personal data […], such as collection, recording, organisation, structuring, storage, adaptation or alteration, retrieval, consultation, use, disclosure by transmission, dissemination or otherwise making available, alignment or combination, restriction, erasure or destruction

Both terms are explicitly very broad. In essence, any data that can somehow be connected to a natural person (the *data subject*) and that a company or other organisation (the *controller*) deals with in some way is covered by the GDPR. This even applies to *pseudonymous* data (Recital 26(2) GDPR), i.e. data that can only be attributed to a person using additional, separately kept information (Art. 5(4) GDPR). Examples for data that can pseudonymously be linked to a person include user IDs and IP addresses. A user ID alone cannot identify a person. But that ID in combination with the database that stores the corresponding user information certainly can. Similarly, most companies will not be able to trace back an IP address to a person on their own. But in combination with the customer data held by the person's ISP, which can potentially be obtained through a court order in many jurisdictions, [this may be possible](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:62014CJ0582).  
Conversely, data that cannot be linked to person, even when consulting additional information sources, is called *anonymous* data and does not fall under the GDPR (Recital 26(5) GDPR). This can include the settings of an application or aggregate statistical data. However, genuine anonymisation that cannot ever be reversed is hard to impossible to achieve. In many cases, [even a handful of seemingly benign data points are enough to uniquely identify a person](https://www.nature.com/articles/s41467-019-10933-3.pdf). Similarly, [fingerprinting can often uniquely identify a device using its settings](https://coveryourtracks.eff.org/about). The GDPR requires taking that into consideration before classifying data as anonymous. And even anonymous data can become personal data if linked with other personal data like a user ID.

Under the GDPR, processing personal data is generally prohibited unless there is a valid legal basis in the law for it. A conclusive list of those is defined in Art. 6(1)(a–f) GDPR. A processing of personal data can only be lawful if it fulfils one of these conditions:

<ol type="a">
    <li>The data subject has given their consent.</li>
    <li>The processing is necessary for performing a contract that the data subject is a party to.</li>
    <li>The processing is necessary for the controller to fulfil a legal obligation that they are subject to.</li>
    <li>The processing is necessary to protect a person’s vital interests.</li>
    <li>The processing is necessary for an official task in the public interest, usually by public authorities.</li>
    <li>The processing is necessary for a legitimate interest of the controller, given it outweighs the data subject’s interests and fundamental rights.</li>
</ol>

In the context of tracking, lit. c), d), and e) are obviously not applicable except in rare exceptions. The GDPR itself does not answer which of the remaining three can be used. For that, one can look to the *data protection authorities* (DPAs). Those are public authorities in each member state tasked with enforcing the GDPR in their respective jurisdiction (Art. 51 GDPR). They publish their interpretation of unclear aspects of the law like this in recommendations. While those recommendations are not legally binding in and of themselves, the DPAs can issue sanctions (including fines) to companies who do not follow them (Art. 58 GDPR).  
According to the data protection authorities, lit. b) and f) [can](https://edpb.europa.eu/sites/default/files/files/file1/edpb_guidelines-art_6-1-b-adopted_after_public_consultation_en.pdf) [typically](https://www.datenschutzkonferenz-online.de/media/oh/20211220_oh_telemedien.pdf) [not](https://www.baden-wuerttemberg.datenschutz.de/wp-content/uploads/2022/03/FAQ-Tracking-online.pdf) be used as a legal basis for tracking, either. That leaves only consent as a potential legal basis for tracking.

In any case and regardless of the type of processing and legal basis used, controllers need to comply with the general principles set forth in the GDPR. Notably, Art. 5(1) GDPR requires that controllers adhere to the principles of *data minimisation* by only processing data to the extent necessary for the particular purpose (lit. c), and *storage limitation* by only keeping stored data in a form that permits the identification of data subjects for at most as long as necessary (lit. e). This is further emphasised by Art. 25(1) GDPR, which prescribes the principle of *data protection by design and by default*.

As an EU law, the GDPR is binding for all companies in the EU. But its territorial scope, as defined in Art. 3 GDPR, also [includes companies outside the EU](https://www.datarequests.org/blog/gdpr-territorial-scope/) if they deliberately process the data of people in the EU related to the offering of goods and services, or for the monitoring of their behaviour, as is the case with tracking.

### Storing and Accessing Information on Terminal Equipment

Another law to consider is the *ePrivacy Directive* (ePD), which went into force back in 2002 and was last amended in 2009.  
As a directive, it is not directly legally binding but needs to be transposed into national law by the member states.

For our purposes, only Art. 5(3) ePD is relevant:

> Member States shall ensure that the storing of information, or the gaining of access to information already stored, in the terminal equipment of a subscriber or user is only allowed on condition that the subscriber or user concerned has given his or her consent, having been provided with clear and comprehensive information […]. This shall not prevent any technical storage or access for the sole purpose of carrying out the transmission of a communication over an electronic communications network, or as strictly necessary in order for the provider of an information society service explicitly requested by the subscriber or user to provide the service.

Unlike the GDPR, Art. 5(3) ePD does not deal with data protection but protects the integrity of a person's terminal equipment. It doesn't just cover personal data but [_any_ data that is read from or stored on a user's device](https://eur-lex.europa.eu/legal-content/en/TXT/?uri=CELEX:62017CJ0673). While this provision is most commonly discussed in the context of cookies (earning the ePD its informal nickname of "the cookie law"), it [also](https://edpb.europa.eu/system/files/2021-04/edpb_guidelines_082020_on_the_targeting_of_social_media_users_en.pdf) [applies](https://www.jipitec.eu/issues/jipitec-5-3-2014/4095) to any other reading or storing of information on a user's device, for example through fingerprinting or tracking pixels.

Also unlike the GDPR, Art. 5(3) ePD does not provide multiple possible legal bases that could apply. There are only two options: Either the reading or storing falls under the exception of being strictly necessary (a clause that has to be interpreted narrowly, with for example [tracking and advertising not being strictly necessary](https://ec.europa.eu/justice/article-29/documentation/opinion-recommendation/files/2012/wp194_en.pdf) despite many publishers’ insistence), or it requires prior informed consent by the user.

For a long time, Germany had not actually properly transposed Art. 5(3) ePD into national law. The national implementation in § 15(3) TMG (*Telemediengesetz*) instead [directly contradicted the ePD](https://www.reuschlaw.de/en/news/in-force-as-of-1-december-2021-the-ttdsg-and-the-new-cookie-rules/), allowing an opt-out mechanism for cookies. In its October 2019 Planet49 decision, the European Court of Justice [ruled](https://eur-lex.europa.eu/legal-content/en/TXT/?uri=CELEX:62017CJ0673) that § 15(3) TMG had to be interpreted in line with Art. 5(3) ePD, [even against the explicit wording of that provision](https://gdprhub.eu/index.php?title=CJEU_-_C-673/17_-_Planet49&oldid=24953).

This finally resulted in Germany changing the law. Since December 2021, Germany implements Art. 5(3) ePD through the *Gesetz zur Regelung des Datenschutzes und des Schutzes der Privatsphäre in der Telekommunikation und bei Telemedien* (TTDSG). In particular, § 25 TTDSG defines privacy protections for terminal equipment. § 25(1) TTDSG mandates that information may only be stored on or accessed from a user's terminal equipment if the user has given consent based on clear and comprehensive information, which is to be provided in accordance with the GDPR. § 25(2) TTDSG then provides two exceptions to that rule, namely if (1) the sole purpose of the storing or access is to carry out the transmission of a communication over a public telecommunications network, or if (2) it is necessary to provide a telemedia service that is explicitly requested by the user.

As such, neither Art. 5(3) ePD nor § 25 TTDSG allow using a contractual necessity or legitimate interest of the controller as a legal basis, placing even stricter conditions on the exception of not needing consent than the GDPR.

### Transferring Personal Data to Third Countries

Finally, we need to consider the case of transferring data to a country outside the EU (a so-called *third country*). The GDPR generally forbids this, unless there is an exception in the law that allows it (Articles 44 – 50 GDPR).

Most simply, transfers to third countries can be based on an *adequacy decision*, which is one of those exceptions (Art. 45 GDPR). As of the time of writing, the European Commission has issued such adequacy decisions for the [following countries](https://ec.europa.eu/info/law/law-topic/data-protection/international-dimension-data-protection/adequacy-decisions_en): Andorra, Argentina, Canada, Faroe Islands, Guernsey, Israel, Isle of Man, Japan, Jersey, New Zealand, Republic of Korea, Switzerland, the United Kingdom, and Uruguay.  
With an adequacy decision, the European Commission attests an adequate level of data protection to the respective country considering the standards of the GDPR. Based on that, data transfers to those countries can happen without any special additional safeguards.

Previously, there was also such an adequacy decision for the United States (where most tracking providers, and many other internet infrastructure companies are based), the *Privacy Shield*. However, the Privacy Shield was invalidated by the European Court of Justice in its July 2020 [Schrems II ruling](https://eur-lex.europa.eu/legal-content/en/TXT/?uri=CELEX:62018CJ0311) due to the overbearing US surveillance programs and lack of effective judicial remedies in the US for data subjects from the EU, just as its predecessor *Safe Harbour* was invalidated in the European Court of Justice's October 2015 [Schrems I ruling](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:62014CJ0362), both over data transfers from Facebook Ireland to the US[^ps2].

[^ps2]: A new "Trans-Atlantic Data Privacy Framework" is in the works as of the time of writing, with an "agreement in principle" having been reached between the [EU](https://ec.europa.eu/commission/presscorner/api/files/attachment/872132/Trans-Atlantic%20Data%20Privacy%20Framework.pdf) and [US](https://www.whitehouse.gov/briefing-room/statements-releases/2022/03/25/fact-sheet-united-states-and-european-commission-announce-trans-atlantic-data-privacy-framework/) but few details having been published and no actual legal documents having been written yet. The announcement has been met with cautious optimism by the [European Data Protection Board](https://edpb.europa.eu/system/files/2022-04/edpb_statement_202201_new_trans-atlantic_data_privacy_framework_en.pdf) and [European Data Protection Supervisor](https://twitter.com/EU_EDPS/status/1507382700575010816), while Max Schrems, the lead litigant behind the Schrems I and II cases [questions](https://noyb.eu/en/privacy-shield-20-first-reaction-max-schrems) whether the new deal actually contains any meaningful changes compared to the previous deals. Regardless, for the time being, controllers cannot rely on an adequacy decision for US transfers.

Thus, legal data transfers to the US are now [significantly harder](https://www.baden-wuerttemberg.datenschutz.de/wp-content/uploads/2021/10/OH-int-Datentransfer.pdf) or [even](https://gdprhub.eu/index.php?title=DSB_(Austria)_-_2021-0.586.257_(D155.027)&oldid=23449) [impossible](https://gdprhub.eu/index.php?title=CNIL_(France)_-_Google_Analytics_(no_case_number)&oldid=23759) in many cases and at the very least require [additional safeguards](https://edpb.europa.eu/system/files/2021-06/edpb_recommendations_202001vo.2.0_supplementarymeasurestransferstools_en.pdf) by the controller.

## Criteria for Compliant Consent Dialogs

Having established that the user's consent is needed for tracking, now we’ll look at the criteria a consent dialog needs to meet in order to be legally compliant. For this purpose, we consider two main legal sources: criteria which are set in actual law, and therefore legally binding, and criteria from recommendations of the data protection authorities (DPAs), which are not directly legally binding but rather echo the DPAs’ interpretation of the law. Some of the criteria from the DPAs have also already been confirmed by court rulings.

Wel'll only consider EU-wide and German sources of law, though DPAs from other EU countries have also issued similar guidance and/or decisions (e.g. the French CNIL in [two](https://www.cnil.fr/fr/cookies-une-vingtaine-organismes-mis-en-demeure) [recommendations](https://www.cnil.fr/fr/cookies-et-autres-traceurs/regles/cookies/lignes-directrices-modificatives-et-recommandation) and one [decision](https://gdprhub.eu/index.php?title=CNIL_(France)_-_SAN-2021-023&oldid=25131), and the Danish [Datatilsynet](https://gdprhub.eu/index.php?title=Datatilsynet_(Denmark)_-_2021-431-0125&oldid=21008)).

### Conditions on Consent from the Law

Any law that restricts data processing in any way can in principle introduce criteria on how to obtain consent, and thus has to be considered here. This most obviously includes all laws already discussed: the GDPR, the ePD, and its national implementation in Germany, the TTDSG.

In addition, the GDPR has *opening clauses*, which allow the member states to introduce national laws that diverge from the GDPR in limited aspects. Germany has made use of these opening clauses in the BDSG (*Bundesdatenschutzgesetz*), which thus also needs to be considered.

However, in actuality, most of these laws do not introduce their own conditions on consent:

* Art. 5(3) ePD delegates to Directive 95/46/EC for how consent has to be implemented. This directive was the predecessor to the GDPR, and has been replaced by it. According to Art. 94(2) GDPR, all references to this repealed directive in previous legislation shall be construed as references to the GDPR.
* § 25(1) TTDSG delegates directly to the GDPR for how consent has to be implemented.
* The BDSG only talks about consent in the context of law enforcement (§ 51 BDSG in combination with § 45 BDSG) and is thus not relevant here.

This leaves the GDPR as the only law that defines applicable conditions for consent dialogs.

Consent is one of the six possible legal bases for processing personal data from Art. 6(1) GDPR. Unsurprisingly, processing that can only rely on consent as a legal basis (like tracking), may thus only happen _after_ consent has been given, and the controller needs to be able to demonstrate that consent has been given (Art. 7(1) GDPR).

Consent itself is defined in Art. 4(11) GDPR, which lists a set of basic conditions an action needs to meet in order to be considered consent, with each being further specified by the recitals to the GDPR:

freely given
:   Consent is not *freely given* if there is a clear imbalance between the data subject and the controller, particularly in the case of public authorities (Recital 43 GDPR). The data subject needs to have a genuine and free choice to refuse (or later withdraw) consent without detriment (Recital 42 GDPR). The provision of a contract or service cannot require a data subject's consent if such consent is not necessary for the performance thereof (Art. 7(4) GDPR; Recital 43 GDPR).

specific
:   For consent to be *specific*, separate consent should be asked for different processing purposes (Recital 32 GDPR).

informed
:   To be *informed*, a request for consent needs to contain at least the identity of the controller and the purposes of the processing (Recital 42 GDPR).

unambiguous
:   Consent is *unambiguous* if the request for it is “clear, concise and not unnecessarily disruptive to the use of the service for which it is provided” (Recital 32 GDPR).

statement or clear affirmative action
:   Silence, pre-ticked boxes, or inactivity do not constitute consent (Recital 32 GDPR). Instead, it has to be given by a statement “which clearly indicates […] the data subject’s acceptance of the proposed processing”, like ticking a checkbox.

Art. 7 GDPR then lists a number of additional conditions for consent:

* If a data subject is asked to give consent through a declaration that also concerns other matters (e.g. also needs to accept a company's terms of service at the same time), the request for consent needs to be “clearly distinguishable from the other matters, in an intelligible and easily accessible form, using clear and plain language” (Art. 7(2) GDPR).
* The data subject needs to be able to withdraw consent at any time (Art. 7(3) GDPR).
* Before giving consent, the data subject needs to be informed that they have the right to withdraw their consent at any time (Art. 7(3) GDPR).
* Later withdrawing consent needs to be as easy as giving it in the first place (Art. 7(3) GDPR).

In addition to that, the GDPR places even stricter conditions on consent for special categories of personal data (this includes, among other things, political opinions, biometric and genetic data, as well as data on a person's health and sex life, Art. 9 GDPR) and third-country transfers without an adequacy decision (Art. 49(1)(a) GDPR), requiring an [express statement, separate for this specific purpose](https://edpb.europa.eu/sites/default/files/files/file1/edpb_guidelines_202005_consent_en.pdf).  
Children under the age of 16 years cannot give consent themselves, it instead needs to be given or authorised by their legal guardians (Art. 8(1) GDPR).

### List of Criteria

Most of the conditions extracted directly from the GDPR are somewhat vague. To alleviate this issue, the data protection authorities publish recommendations which detail their interpretation of the law and provide specific guidelines on how to follow them.

I have searched all current publications regarding consent and adjacent topics from all German state data protection authorities, as well as the national DPA, the German data protection conference (*Datenschutzkonferenz*, a council of the German DPAs that develops unified recommendations), and the European Data Protection Board (an EU body tasked with ensuring consistent application of data protection law across the EU) for criteria on consent dialogs. The list below consolidates the criteria from the GDPR and DPA recommendations. Click an element to view the corresponding sources. Where the criteria have already been confirmed by courts, I cite those rulings as well.

It should be emphasised that *any* violation against even a single one of these criteria results in all data processing based on that supposed consent being illegal.

#### Criteria for Underlying Circumstances

<details>
  <summary>Consent needs to be given through a clear, affirmative action like clicking a button or ticking a checkbox.</summary>
  {{% md %}}
  * Recital 32 GDPR
  * [Planet49 ruling]
  * [LG Rostock - 3 O 762/19]
  * [EDPB Guidelines 05/2020 on consent], para. 80
  * [LfD Niedersachsen Handreichung Consent-Layer]
  * [LfDI BaWü Tracking FAQ], no. A.4.2
  * [DSK OH Telemedien], p. 13
  {{% /md %}}
</details>
<details>
  <summary>Processing that needs to rely on consent may only happen after consent has been given.</summary>
  {{% md %}}
  * Art. 7(1) GDPR
  * [EDPB Guidelines 05/2020 on consent], para. 90
  * [LfD Niedersachsen Handreichung Consent-Layer]
  * [LfDI BaWü Tracking FAQ], no. B.1.1.1
  * [DSK OH Telemedien], p. 12
  * [Fashion ID ruling]
  * [LG Frankfurt am Main - 3-06 O 24/21]
  {{% /md %}}
</details>
<details>
  <summary>Consent has to be voluntary, i.e. it needs to be possible to use the website/app without consenting.</summary>
  {{% md %}}
  * Recital 42 GDPR
  * [LfDI BaWü Tracking FAQ], no. A.4.2
  * [DSK Kurzpapier 20]
  {{% /md %}}
</details>
<details>
  <summary>It must be possible to later withdraw consent at any time and this has to be as easy as giving consent in the first place. The data subject needs to be informed of this before giving consent.</summary>
  {{% md %}}
  * Art. 7(3) GDPR
  * [EDPB Guidelines 05/2020 on consent], para. 114
  * [LfD Niedersachsen Handreichung Consent-Layer]
  * [LfDI BaWü Tracking FAQ], no. B.1.6
  * [DSK OH Telemedien], p. 18
  {{% /md %}}
</details>
<details>
  <summary>A consent dialog may not make it impossible to access other required legal notices (like contact information or privacy policy).</summary>
  {{% md %}}
  * [LfDI BaWü Tracking FAQ], no. A.4.1
  {{% /md %}}
</details>

#### Criteria for Wording and Design of Consent Dialogs

<details>
  <summary>The consent dialog needs to have a clear heading that accurately describes the impact of the processing on the data subject, like “Data disclosure to third parties for tracking purposes.” Vague headings like “We respect your privacy.” are not sufficient.</summary>
  {{% md %}}
  * [LfDI BaWü Tracking FAQ], no. B.1.3.7
  {{% /md %}}
</details>
<details>
  <summary>The “consent” button cannot be highlighted compared to the “refuse” button (e.g. by making it bigger or using a more prominent colour for it).</summary>
  {{% md %}}
  * [LG Rostock - 3 O 762/19]
  * [LfD Niedersachsen Handreichung Consent-Layer]
  * [LfDI BaWü Tracking FAQ], no. A.4.3
  * [BayLDA Pressemitteilung Länderübergreifende Prüfung]
  * [LfD Niedersachsen TTDSG FAQ]
  {{% /md %}}
</details>
<details>
  <summary>The consent notice must be in the language of the country it addresses.</summary>
  {{% md %}}
  * [LfDI BaWü Tracking FAQ], no. B.1.3.1
  {{% /md %}}
</details>
<details>
  <summary>The consent notice cannot be overly long or complex.</summary>
  {{% md %}}
  * [LfDI BaWü Tracking FAQ], nos. B.1.3.3.3, B.1.3.3.4
  {{% /md %}}
</details>
<details>
  <summary>A consent notice needs to be clearly distinguishable from other matters like regular terms of service.</summary>
  {{% md %}}
  * Art. 7(2) GDPR
  * [EDPB Guidelines 05/2020 on consent], para. 81
  * [LfDI BaWü Tracking FAQ], no. B.1.5.1
  {{% /md %}}
</details>
<details>
  <summary>A consent notice that only mentions cookies can only receive consent under the ePD, not the GDPR</summary>
  {{% md %}}
  * [LfDI BaWü Tracking FAQ], no. B.1.3.5.1
  * [DSK OH Telemedien], p. 9
  {{% /md %}}
</details>

#### Criteria on Information to Include in Consent Dialogs

<details>
  <summary>The consent notice needs to contain at least the following details: Who is the controller?, What is the purpose of the processing?, If cookies are used, what is their duration?, Is there any access for third parties?</summary>
  {{% md %}}
  * Recital 42 GDPR
  * [Planet49 ruling]
  * [LfDI BaWü Tracking FAQ], no. A.4.2
  * [DSK OH Telemedien], p. 12
  {{% /md %}}
</details>
<details>
  <summary>Third-party recipients have to be mentioned explicitly.</summary>
  {{% md %}}
  * [LfD Niedersachsen Handreichung Consent-Layer]
  * [LfDI BaWü Tracking FAQ], no. A.4.2
  {{% /md %}}
</details>
<details>
  <summary>The consent notice needs to list concrete purposes, vague wordings like “to improve user experience” are not sufficient.</summary>
  {{% md %}}
  * [LfD Niedersachsen Handreichung Consent-Layer]
  * [LfDI BaWü Tracking FAQ], no. A.4.2
  * [DSK OH Telemedien], p. 16
  {{% /md %}}
</details>

#### Criteria for Buttons and Interactive Elements in Consent Dialogs

<details>
  <summary>Refusing consent has to be possible through inaction or with the same number of clicks as consenting.</summary>
  {{% md %}}
  * [LfD Niedersachsen Handreichung Consent-Layer]
  * [LfDI BaWü Tracking FAQ], no. A.4.3
  * [DSK OH Telemedien], p. 14
  * [BayLDA Pressemitteilung Länderübergreifende Prüfung]
  {{% /md %}}
</details>
<details>
  <summary>A button with the text “Okay” does not sufficiently convey that clicking it is supposed to agree to the consent dialog, and thus does not result in valid consent</summary>
  {{% md %}}
  * [LfD Niedersachsen Handreichung Consent-Layer]
  * [LfDI BaWü Tracking FAQ], no. B.1.3.12.1
  * [DSK OH Telemedien], p. 14
  {{% /md %}}
</details>
<details>
  <summary>It is not possible to receive consent on a page that doesn’t include all necessary details (e.g. if they are hidden behind another link, or on a page deeper in the consent flow).</summary>
  {{% md %}}
  * [LfD Niedersachsen Handreichung Consent-Layer]
  * [DSK OH Telemedien], p. 14
  {{% /md %}}
</details>
<details>
  <summary>It needs to be possible to only consent to adequate subpurposes and/or recipients.</summary>
  {{% md %}}
  * Recital 32 GDPR
  * [EDPB Guidelines 05/2020 on consent], para. 42
  * [LfDI BaWü Tracking FAQ], no. A.4.2
  * [DSK OH Telemedien], p. 16
  {{% /md %}}
</details>
<details>
  <summary>No purposes may be pre-selected.</summary>
  {{% md %}}
  * Recital 32 GDPR
  * [Planet49 ruling]
  * [LG Rostock - 3 O 762/19]
  * [LfDI BaWü Tracking FAQ], no. A.4.2
  {{% /md %}}
</details>
<details>
  <summary>Clicking an “Accept all” button may not toggle additional, previously unselected purposes.</summary>
  {{% md %}}
  * [LfD Niedersachsen Handreichung Consent-Layer]
  {{% /md %}}
</details>
<details>
  <summary>A consent dialog that saves consent but not refusal thereof (and is thus displayed over and over again when refused) is not compliant.</summary>
  {{% md %}}
  * [LfDI BaWü Tracking FAQ], no. B.2.2.3
  {{% /md %}}
</details>

[Planet49 ruling]: https://eur-lex.europa.eu/legal-content/en/TXT/?uri=CELEX:62017CJ0673
[LG Rostock - 3 O 762/19]: https://gdprhub.eu/index.php?title=LG_Rostock_-_3_O_762/19&oldid=19832
[EDPB Guidelines 05/2020 on consent]: https://edpb.europa.eu/sites/default/files/files/file1/edpb_guidelines_202005_consent_en.pdf
[LfD Niedersachsen Handreichung Consent-Layer]: https://lfd.niedersachsen.de/download/161158
[LfDI BaWü Tracking FAQ]: https://www.baden-wuerttemberg.datenschutz.de/wp-content/uploads/2022/03/FAQ-Tracking-online.pdf
[DSK OH Telemedien]: https://www.datenschutzkonferenz-online.de/media/oh/20211220_oh_telemedien.pdf
[Fashion ID ruling]: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:62017CJ0040
[LG Frankfurt am Main - 3-06 O 24/21]: https://openjur.de/u/2378854.html
[BayLDA Pressemitteilung Länderübergreifende Prüfung]: https://www.lda.bayern.de/media/pm/pm2021_06.pdf
[LfD Niedersachsen TTDSG FAQ]: https://lfd.niedersachsen.de/startseite/infothek/faqs_zur_ds_gvo/faq-telekommunikations-telemediendatenschutz-gesetz-ttdsg-206449.html
[DSK Kurzpapier 20]: https://datenschutzkonferenz-online.de/media/kp/dsk_kpnr_20.pdf

<style>
details ul { margin: 0; }
</style>
