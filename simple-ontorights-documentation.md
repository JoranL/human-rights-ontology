[Back to home page](index.md)

[Access OntoRights](ontorights-access.md)

# Easy OntoRights Manual
The purpose of this manual is to facilitate for human rights practitioners who want to adapt the human rights ontology OntoRights to a conceptual model tailored to the needs of a specific organisation. HURIDOCS’ community resource “Plan for the information you need” explains more about the benefits of databases and basics of conceptual modelling. Easy OntoRights can be accessed as a local website. Section 1-3 is repeating the most essential information from the master thesis that led to the design of OntoRights. For a full understanding, it is of course better to read the complete original master thesis ([pdf](files/Lindeberg 2022 Ontology Design Master Thesis.pdf) or [Google Doc](https://docs.google.com/document/d/1JL03YWWXHXQJ5mIXPPwEcz7l_mkSwAsA4XO4uh1uba0/edit?usp=sharing)),

## About Easy OntoRights
The purpose of a OntoRights is twofold:
1. To have a well-founded and comprehensive conceptual model (ontology), in which parts can be reused.
2. To facilitate integration between databases.

The OntoRights builds on Unified Foundational Ontology (UFO), and some of its core ontologies, most prominently UFO-L (L as in Legal). Thereby, it reuses well-founded and widely used patterns. However, the full version of OntoRights (Full OntoRights) is rather complex, which limits its usefulness for modelling concrete databases for human rights groups with often limited resources. Therefore, OntoRights also exists in a simplified version (Easy OntoRights) that is much closer to the structure of a relational database.

## Delimitations of the Manual
The manual does not cover how to identify your needs and important concepts. This can be done by for example following HURIDOCS’ community resource until step 4.1.The manual does not cover how to implement a conceptual model into a physical data model (including for example how to handle sub-classes, assign foreign keys, and so-called association tables to handle many-to-many relations). Nor does in address general systems management challenges such as data migration, user access privileges, or management of information security and privacy.

## How Easy OntoRights was Designed
In short, the following steps were taken to design OntoRights:
1. Initial discussions with HURIDOCS and a literature review.
2. A document survey of the content of parts of the OHCHR Human Rights Monitoring Manual and HURIDOCS’ Events Standard format, in order to get a comprehensive view of the relevant concepts and corresponding relations. More than 500 concepts were identified.
3. The document survey was analysed in order to group the concept info subdomains.
4. This was the base for a questionnaire to human rights practitioners, with the aim of understanding the importance of the different subdomains and so-called competency questions.
5. During the design of OntoRights, an effort was made to reuse existing ontologies. Also reference data from for example the Universal Human Rights Index and HURIDOCS Microthesauri was reused. Since most human rights groups will probably only need parts of OntoRights, it was designed in modules.
6. Another aspect of reuse is that some of the suggested attributes for Easy OntoRights are URLs to important external databases, such as Geonames or WhoWasinCommand.7. OntoRights was designed and published with OntoUML Visual Paradigm Plugin.

## How to Interpret Easy OntoRights
It is expected that the reader of this manual has a basic understanding of UML class diagrams. Otherwise, a short introduction is needed.Note that the connection between from Easy OntoRights to Full OntoRights is represented with so-called stereotypes within “&lt;>” and that the connection to OntoUML, the ontology modelling language that bridges UML and UFO, is represented stereotyped within “&lt;&lt;>>”. Both these stereotypes can be ignored in classes as well as associations.A particular aspect of UFO is that **material** relations is mediated by a **relator** class, which may appear redundant. The modules of Easy OntoRights consist of nine ordinary modules and an annex with data types and enumerations (lists). Module 1 of human rights violations can be considered the core module.The modules are in fact different diagrams of the same model. Some classes appear in more than one module. Each class is explained in the module with its so-called master view (marked with an **M** or nothing, as opposed to an **a**).Below, each class is explained. For someone that has already read Part V of the thesis, parts of the information will be repeated. The attributes will normally not be explained, but worth considering for better understanding. Some attributes have as values data types and enumerations that can be found in the Easy OntoRights Annex diagram. Note that some attributes are not self-explanatory (but on the other hand not essential) since they have to do with the relation to Full OntoRights.

### Module 1: Human Rights Violation
This module can be considered the core module.While **Event** expresses what happened in a certain situation, **Human Rights Violation** expresses the legal human rights implications of an Event. (Read more about Event in Module 2).A Human Rights Violation always must include at least one **Perpetrator** and at least one **Victim**, who in turn are **Agents**, either persons or some kind of collective (see agentType). A Human Rights Violation can be a case of **Legally Defined Human Rights Violation** e.g. torture or enforced disappearance, which have specific definitions. A Human Rights Violations normally concerns one or more **Human Rights Standard** and/or **Human Rights Instrument**. A Human Rights Standard is normally described in a Human Rights Instrument.Events and their properties, including any associated Human Rights Violation, are clarified through a **Monitoring Process**.

### Module 2: Actions and Consequences
This module is for expressing what happened, in other words “who did what to whom” (on a material level, as opposed to the human rights implications expressed in Module 1).An **Event** is often part of a larger Event. One or many Events can cause one or many Events. An Event is performed by exactly one **Agent**. An Event can have **Consequence For Agent**.This structure allows and encourages events to be expressed on a very detailed level. For instance, if a police officer fires a teargas grenade against a group of five people, this can be represented as one event that directly causes five resulting events when people inhale the smoke. They are all part of one larger event. If this level of detail is not needed, the group can for example be expressed as a collective instead of five individuals, or perhaps just the firing of the grenade could be registered. In this case, the resulting events can be omitted, but the first event can still be associated with Consequence for Agent.An Event may be important enough to have its **Consequence For Agent** represented. An intentional Event can also have Consequence For Agent as an intended effect.Finally, an Event happens in a **Place**.

_Note for adjustments_: You could consider making this module less complex (but also less expressive) by removing the intended effect association. If you want to express types of roles of Agents in Events, this can be done with the intendedRole and actualRole attributes in Event, complemented with intended and actual Consequence For Agent.

### Module 3: Agents and Memberships
An **Agent** is either a **Person** or a **Organisation Or Group**, i.e any kind of collective. A Person can be a **Member** and have **Membership** of an Organisation Or Group. Any Agent can be active in one or more **Place**, and a person is also born in a Place. A Person can have a great number of different **Person Relationship** to other Persons (it is not called “personal relationship” to convey that it can also be for example work relations). Finally, Human Rights Mechanism is a type of **Organisation Or Group**.

### **Module 4: Organisations and Networks
An **Organisation Or Group** can be part or a larger Organisation Or Group. For example, an organisational unit is part of another organisational unit, which is part of a state authority, which is part of the Kingdom of Sweden.Any type of **Agent** can have different types of **Network Connection** to other Agents.An Organisation Or Group can have, for example own or manage, a **Site**, such as an office or a prison.

### Module 5: Places
A **Place** is usually part of one or more larger Places. For example, Paris is part of France, and Russia is part of both Europe and Asia. A particular type of Place is a **Site**, which is for example an apartment, building, or complex of building, usually with a specific purpose, for example to function as a **Detention Centre**. An **Event** or **Situation** happens within a **Place**.

### Module 6: Detention Centres
A **Site** can function as a **Detention Centre**. Within a Detention Centre, a number of Detainment Conditions can exist (for example, in different sections). Both **Detained Person** and **Detained Group** can be held in a Detention Centre. (All groups are of course composed by persons, but it is sometimes more practical to register whole groups as detained. Note that Module 2 may be better to use to express concrete abusive events against a person or group.

  _Note for adjustments_: If you do not have to represent detained collectives (Organisation Or Group), the complexity of this module can be reduced significantly by excluding Organisation Or Group, Detained Group, Agent, Membership, and Member, and then also changing the **affects** association from Agent to Detained Person.

### Module 7: Human Rights Protection System
The contents of this module was partly explained in Module 1. A **Human Rights Instrument** can be part of another Human Rights Instrument. For example, Article 1 of the Universal Declaration of Human Rights is part of the Universal Declaration of Human Rights, and the Universal Declaration of Human Rights is part of the International Bill of Human Rights.A **Legally Defined Human Rights Violation** is defined by a number of Human Rights Instruments and/or **Human Rights Standards**. The mandate of a**Human Rights Mechanism** is defined by a Human Rights Instrument.

### Module 8: Monitoring and Information Management
When a human rights group becomes interested in one or many related **Event**, a human rights staff person will open a **Monitoring Process** (can also be called a case file) and register what is known about the Event. However, the knowledge about what happened is acquired through **Monitoring Events**. Like any Event, A Monitoring Event can be decomposed into sub-events for increased granularity.A Monitoring Event occurs within a **Place**, and involves one or many **Monitoring Event Participants**, which must have a **participantRole**, for example witness, victim or alleged perpetrator. A Monitoring Event Participant is always a Person, that in the context of that event can represent an **Organisation Or Group**. The Monitoring Event has as a **confidentiality** attribute, that depends both on the informedConsent that was obtained, and the estimation done by the monitoring staff person (see also the Confidentiality Management data type in Easy OntoRights Annex). Note that the Monitoring Event does not contain the actual information that was acquired. The actual information is registered as one or more Information Piece. One reason is that different **Information Pieces** may be assigned different confidentiality levels. Also, while the confidentiality attribute of a Monitoring Event refers to that the event at all happened, the confidentiality attribute of an Information Piece refers to actual information that was obtained.The content of an Information Piece may be written as a string value of the **description** attribute, but may also exist as a digital file, that was for example received as an attachment to a message.

_Note for adjustments_: Just like any other Events, Monitoring Events can in real life have intended and real **Consequences For Agent** (see Module 2). Therefore, it would be logical to represent Monitoring Event as a subclass of Event. This would better express how the monitoring of a human rights group shares common aspects with any other event that affects a situation. However, mixing the actions of the human rights group with the actions of others can also be complex, which is why this possibility was discarded.

### Module 9: Legal Process
An **Official Legal Process**, such as a criminal investigation, may have negative as well as positive consequences for someone.An Official Legal Process can be associated with another Official Legal Process. For example, a police investigation may result in a court case. An Official Legal Process is composed of **Official Legal Records**, that in turn are created by an **Event**, issued by an **Agent**, may have content that refers to an Agent, and is part of a **Consequence For Agent**.

_Note for adjustments_: This module can be seen as a submodule of Module 2, but can also stand alone, including only Official Legal Record, Official Legal Process, and Legal Process Relation.

## How to Adapt Easy OntoRights to a Tailored Conceptual Data Model
1. Study the diagram of each module and read about them in the section above for better understanding.
2. Decide the tool you will use. Most efficient is probably to open the Easy OntoRights project with the above-mentioned Plugin for Visual Paradigm. Another tool that is easy to use is Diagrams.net.
3. Select the modules that contain your identified concepts.
4. Consider if there are classes in the selected modules that you do not need. If so, exclude them. Note that in some situations you might have to redesign the module slightly after excluding a class.
5. Adapt the multiplicity between classes if needed.
6. Adapt the attributes according to your needs. Note that some of the enumerations visible in the Easy OntoRights Annex diagram contain links to HURIDOCS Microthesauri reference data, and that the Microthesauri contain even more useful datasets.
7. Now you should have your conceptual model.
