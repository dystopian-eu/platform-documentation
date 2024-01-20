# Party

*Party as a Person*

    Definition: When a party is a person, it refers to an individual human being. This could be a user, customer, client, or any individual who interacts with or is managed by the system.
    Attributes: In the database, a party that is a person might have attributes such as name, date of birth, contact details, personal identification numbers, and possibly relationships to other parties (e.g., family members, business associates).
    Use Case: In a customer relationship management system, for example, a party as a person would represent individual customers, each with unique personal details and histories of interaction with the organization.

*Party as an Entity*

    Definition: When a party is an entity, it refers to a group, organization, company, or any form of collective that can engage in contracts or transactions. An entity is typically a legal construct that has rights and responsibilities.
    Attributes: For a party that is an entity, the database might store attributes like business name, registration number, industry type, contact details of key representatives, and details about its legal and contractual relationships.
    Use Case: In business applications, a party as an entity could represent client companies, suppliers, partner organizations, or government bodies with whom the system's user or owner has a relationship.

*Common Characteristics*

    Global Identifier: Both types of parties would have a global identifier (global_id) in a distributed system, allowing them to be uniquely identified across multiple instances or components of the system.
    Contracts and Relationships: Both can have associated contracts (contracts_list) and relationships (relationships_list), which are stored in a flexible JSONB format to accommodate various data structures.
    Metadata: Additional information specific to the party, whether a person or an entity, can be stored in the Party_Metadata table, allowing for extended attributes not covered in the main Party table.

    This distinction between person and entity is crucial for systems that manage a wide range of interactions and relationships, ensuring that the data model can accommodate the diverse nature of parties involved in any business or organizational context.


*Entity: Party*

    - party_id: This is the primary key of the table, of type bigint. It uniquely identifies each party within the system. This field is not nullable, meaning every record in the table must have a party_id.

    - global_id: A varchar(32) field that seems to store a global identifier for the party. This is likely used to uniquely identify a user across different instances of the system. The format mentioned suggests it could be a combination of the party_id and an instance identifier (e.g., party_id:instance_id).

    - party_type: A varchar(50) field to specify the type of the party. The exact values this might hold are not specified, but it could include types like 'individual', 'organization', etc.

    - contracts_list: This is a jsonb field, allowing for the storage of JSON objects. It can be used to store a list of contracts associated with the party. The use of JSONB provides flexibility in the data structure.

    - contracts_list_type: Accompanying the contracts_list, this varchar(50) field likely describes the type or nature of the contracts listed.

    - products_bundle: Another jsonb field, possibly used to store information about various products or services bundled with the party.

    - relationships_list: This jsonb field could be used to store relationships the party has, which could include relationships with other parties, entities, or services.

    - relationships_list_type: A varchar(50) field that might describe the type of relationships stored in relationships_list.

    - legal_entity_list: This jsonb field is possibly used to store a list of legal entities associated with the party.

    - characteristics_ref: Another jsonb field that could store various characteristics or attributes of the party.

    - status: A varchar(50) field to denote the current status of the party. This could include values like 'active', 'inactive', 'suspended', etc.

    - Metadata: Model extension to allow the adding of characteristics for the Party or Entity. This is a key value Pair Model.

    

**Table: Party_Metadata**

    - party_id: This is a foreign key to the Party table, establishing a one-to-one relationship. Each record in the Party_Metadata table corresponds to a record in the Party table. It's the primary key of this table as well.

    - metadata: A jsonb field intended to store additional metadata about the party. This could include any extra information that doesn't fit into the Party table's structure.



**Based Table defintion :**

```

CREATE TABLE "lagertha_party"."Party" (
	party_id bigint primary key not NULL,
	global_id varchar(32) NULL,
	party_type varchar(50) NULL,
	contracts_list jsonb NULL,
	contracts_list_type varchar(50) NULL,
	products_bundle jsonb NULL,
	relationships_list jsonb NULL,
	relationships_list_type varchar(50) NULL,
	legal_entity_list jsonb NULL,
	characteristics_ref jsonb NULL,
	status varchar(50) NULL
);

CREATE TABLE "lagertha_party"."Party_Metadata" (
	party_id bigint primary key not NULL,
	metadata jsonb NULL
);

```


**Party_type**
--
Allowable Values

- PERSONAL
- NON_PERSONAL

**Contracts List**
--
```

```