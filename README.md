#Standard RDF representation for glycans

The following document describes a standard RDF representation for glycan related data. 
Subject
Classesfoaf
Properties
Sequence information and identifier
Resource properties
Images
Compositions
Biological source
Publication references
Experimental data
Glyco relationship RDF
Monosaccharide information
Other Glycan information
Glycan Function
Description of GlycoProtein
RDFsized glyco-DBs available for SPARQL search -1
RDFsized glyco-DBs available for SPARQL search -2
other RDFs necessary for SPARQL examples
References and Links
Subject
Each document consists of one or several glycans which in the XML version are described using Description tags with each specifying the of the RDF triples in the about attribute. 
Classes
Each class name (e.g.) will translate in RDF to:

```
@prefix glyco: <http://purl.jp/bio/12/#> .
```

##Table 1.
<table>
  <tr><th>owl:class</th>		<th>rdfs:label</th>			<th>rdfs:subClassOf</th>	<th>rdfs:comment</th><th></tr>
  <tr><td>cyclic_glycan</td>		<td>Cyclic glycan</td>			<td>glycan</td>			<td></td></tr>
  <tr><td>repeat_unit</td>		<td>Repeating glycan structure</td>	<td>glycan</td>			<td></td></tr>
  <tr><td>biological_repeat_unit</td>	<td></td>				<td>repeatingGlycan</td>	<td></td></tr>
</table>

##Table 2.
<table>
  <tr><td>sequence</td>			<td>biomolecule sequence</td>		<td>glycan</td>			<td></td></tr>
  <tr><td>glycosequence</td>		<td>glycan sequence</td>		<td>sequence</td>		<td></td></tr>
  <tr><td>glycoconjugate_sequence</td>	<td>glycoconjugate sequence</td>	<td>sequence</td>		<td></td></tr>
  <tr><td>aglycon</td>			<td>the aglycon portion of a glycoconjugate</td><td></td>		<td>can be used in combination with other rdf:types from other ontologies.</td></tr>
</table>

##Table 3.
<table>
  <tr><td>synthetic</td>		<td>synthetic glycan</td>		<td>glycan</td>			<td></td></tr>
  <tr><td>modified</td>			<td>modified glycan</td>		<td>glycan</td>			<td>including degradation products</td></tr>
  <tr><td>chemical_synthetic</td>	<td/>					<td>synthetic</td>		<td/></tr>
  <tr><td>enzymatical_synthetic</td>	<td/>					<td>synthetic</td>		<td/></tr>
  <tr><td>chemoenzymatical_synthetic</td><td/>					<td>synthetic</td>		<td/></tr>
  <tr><td>chemical_modified</td>	<td/>					<td>modified</td>		<td/></tr>
  <tr><td>enzymatical_modified</td>	<td/>					<td>modified</td>		<td/></tr>
  <tr><td>modeled</td>			<td/>					<td></td>			<td/></tr>
  <tr><td>natural</td>			<td>natural glycan</td>			<td>glycan</td>			<td/></tr>
</table>

##Table 4.
<table>
  <tr><td>database</td>			<td>a database</td>			<td></td>			<td></td></tr>
  <tr><td>glycan_database</td>		<td>a glycan database</td>		<td>database</td>		<td>http://purl.jp/bio/12/core/database.rdf</td></tr>
</table>




Properties
Each property name (e.g. sequence_glyde, link_to_ccsd) in the following tables (left column) will translate in RDF to:
```
@prefix glyco: <http://purl.jp/bio/12/> .
subjectURI
glyco:sequence_glyde “…”;
glyco:link_to_ccsd <http://www.genome.jp/dbget-bin/www_bget?carbbank+6915> .
```
1. Sequence information and identifier
The following table describes properties that have simple data types as object (e.g. Strings, Integer).
To have at least one of the sequence formats is mandatory.

##Table 4.
<table>
  <tr><th>predicate</th>		<th>data type</th>	<th>comment</th></tr>
  <tr><td rowspan="2">rdf:type</td>			<td>class</td>		<td>glycan class (N-glycan, O-glycan, etc.) - from GlycO or some glyco-ontology</td></tr>
  <tr><td>(glyco:repeatUnit, glyco:biologicalRepeatUnit, glyco:cyclicGlycan)</td></tr>
  <tr><td>dcterms:identifier</td>	<td>xsd:string</td>	<td>entry ID in other resource</td></tr>
  <tr><td>foaf:name</td>		<td>xsd:string</td>	<td>Trivial name (eg sialyl-lewis-x, lactosamine)</td></tr>
  <tr><td>has_glycosequence</td>	<td>Resource</td>	<td>glycan sequence information to object of rdf:type glyco:sequence</td></tr>
  <tr><td>has_glycoconjugate_sequence</td><td>Resource</td>	<td>sequence information to ojbect of rdf:type glyco:glycoconjugate_sequence</td></tr>
  <tr><td>has_aglycon</td>		<td>Resource</td>	<td>in case of glyco_conjugate, define the aglycon</td></tr>
  <tr><td>has_repeat_count<td>		<td>Resource</td>	<td/></tr>
</table>

##Table 5. has_aglycon node predicates
<table>
  <tr><th>predicate</th>		<th>data type</th>	<th>comment</th></tr>
  <tr><td>rdf:type</td>			<td>class</td>		<td>ChEBI (http://www.ebi.ac.uk/chebi/downloadsForward.do)</td></tr>
  <tr><td>foaf:name</td>			<td>xsd:string</td>	<td>trivial name</td></tr>
  <tr><td>has_reference</td>		<td>blank node</td>	<td>see Reference</td></tr>
  <tr><td>attachment_position</td>	<td>xsd:Integer</td>	<td>atom number in aglycon</td></tr>
  <tr><td>linkage</td>			<td>xsd:Integer</td>	<td>carbon number in glycan</td></tr>
</table>


has_repeat_count is applicable only if a structure encoded in the sequence IS a repeating unit
##Table 6. has_repeat_count node
<table>
  <tr><th>predicate</th>		<th>data type</th>	<th>comment</th></tr>
  <tr><td>repeat_attribute</td>		<td>repeat</td>	<td>(min, max, exact, average, unknown) part of has_repeat_count blank node</td></tr>
  <tr><td>repeat_count</td>		<td>xsd:integer</td>	<td>value of repeat_attribute in blank node  (use if it is known)</td></tr>
</table>

##Table 7. sequence formats property of the glyco:sequence blank node
<table>
<tr><th>predicate</th>		<th>data type</th>	<th>comment</th></tr>
<tr><td>rdf:type</td>		<td>owl:class</td>	<td>sequence</td></tr>
<tr><td>in_glycoct</td>		<td>xsd:String</td>	<td>plain literal string with the carbohydrate sequence in GlycoCT condensed format. GlycoCT sequence format is described in a reference <a href="http://www.ncbi.nlm.nih.gov/pubmed/18436199"/>18436199</a></td></tr>
<tr><td>in_KCF</td>		<td>xsd:String</td>	<td>String with the carbohydrate sequence in KCF format.</td></tr>
<tr><td>in_GlydeII</td>		<td>xsd:String</td>	<td>String with the carbohydrate sequence in Glyde-II format. </td></tr>
<tr><td>in_linearCode</td>	<td>xsd:String</td>	<td>String with the carbohydrate sequence in LinearCode® format.</td></tr>
<tr><td>in_linucs</td>		<td>xsd:String</td>	<td>String with the carbohydrate sequence in LINUCS format. </td></tr>
<tr><td>in_IUPAC_condensed</td>	<td rowspan="3">xsd:String</td>	<td rowspan="3">String with carbohydrate sequence in IUPAC nomenclature. 
http://www.chem.qmul.ac.uk/iupac/
http://www.chem.qmul.ac.uk/iupac/misc/glycp.html
http://www.chem.qmul.ac.uk/iupac/misc/glylp.html</td></tr>
<tr><td>in_IUPAC_short</td></tr>
<tr><td>in_IUPAC_extended</td></tr>
<tr><td>in_SweetDB</td>		<td>multiline String</td>	<td>String with carbohydrate sequence in Sweet-DB pseudographics.</td></tr>
<tr><td>in_CSDB</td>		<td>xsd:String</td>	<td>String with sequence of residues in CSDB linear code
http://csdb.glycoscience.ru/bacterial/core/help.php?db=bacterial&amp;topic=rules</td></tr>
</table>

```text/turtle
@prefix glycoSequence:  <http://purl.jp/bio/12/glycanSequence/0.1/> .
@prefix glyco:   <http://purl.jp/bio/12/> .
@prefix foaf:   <http://xmlns.com/foaf/0.1/>

<http://www.glycome-db.org/rdf/2015>
      glyco:has_glycosequence    <http://www.glycome-db.org/rdf/2015#UUID> ;
      glyco:has_glycoconjugate_sequence <http://www.glycome-db.org/rdf/2015#UUID2> ;
      glyco:has_aglycon 
       [ rdf:type  glyco:aglycon;
          rdf:type chebi:lipid ;
          rdfs:seeAlso <>  # Link to database (eg.CheBI, PubChem)
          foaf: name;    #free text
          glyco:attachment_position 3;	#atom number in aglycon
          glyco:linkage 1		#carbon number in glycan
       ] ;
      rdf:type  glyco:GlycanClass ;
     glyco:relation <http://...>	#back-reference to relastionship RDF
.
<http://www.glycome-db.org/rdf/2015#UUID>    #UUID is a random literal to make blank nodes available from SPARQL
       rdf:type	glyco:glycosequence ;
       glyco:in_linucs              "[][?-D-GlcNAc]{[(3+1)][a-L-Fucp]{}[(4+1)][b-D-Galp]{[(2+1)][a-L-Fucp]{}}}" ;
       glyco:in_iupac              "..” .
<http://www.glycome-db.org/rdf/2015#UUID2>
      glyco:rdf:type	glyco:glycoconjugate_sequence ;
      glyco:in_linucs             "[XXX][?-D-GlcNAc]{[(3+1)][a-L-Fucp]{}[(4+1)][b-D-Galp]{[(2+1)][a-L-Fucp]{}}}" .
```

#Resource properties

The following table contains information about links to other non-RDF resources describing the same carbohydrate.  
All reference databases must be listed in http://purl.jp/bio/12/database.rdf  (currently under construction).
databases of  glycan database https://docs.google.com/document/d/1xy3N7Njsm0EO9fjjp3GC-wuDG3TPcUGQnGPdltp0YpI/edit

##Table 8. Describing a glycan database
<table>
<tr><td>is_glycan_database</td>		<td>Resource</td>	<td>URI (Range is glyco:glycan_database class )</td></tr>
<tr><td>dcterms:identifier</td>		<td>xsd:String</td>	<td>entry ID in other resource</td></tr>
<tr><td>rdfs:seeAlso</td>		<td>Resource</td>	<td>URI Reference to other resource can be used as subject for further annotation (resource_name and resource_id)</td></tr>
<tr><td>owl:sameAs</td>			<td>Resource</td>	<td>URI Reference to another RDF description of exactly this carbohydrate provided by a different resource which may contain complementary information</td></tr>
</table>

``text/turtle
@prefix glyco:   <http://purl.jp/bio/12/> .
@prefix glycodb:   <http://purl.jp/bio/12/database> .

<http://www.glycome-db.org/rdf/2015>
     rdfs:seeAlso <http://csdb.glycoscience.ru/bacterial/core/search_id.php?id_list=0538> ;
     rdfs:seeAlso <http://csdb.glycoscience.ru/bacterial/core/search_id.php?id_list=23173>;
     rdfs:seeAlso <http://www.genome.jp/dbget-bin/www_bget?carbbank+14848">;
     rdfs:seeAlso <http://www.ebi.ac.uk/eurocarb/show_glycan.action?glycanSequenceId=2711>;
     rdfs:seeAlso <http://www.glycosciences.de/sweetdb/start.php?action=explore_linucsid&linucsid=2611&show=1#struct%0A%20%20%09%09>;
     rdfs:seeAlso <_:1> .

<http://csdb.glycoscience.ru/bacterial/core/search_id.php?id_list=0538>
glyco:is_glycan_database glycodb:bcsdb; 
dcterms:identifier “0538".
<http://csdb.glycoscience.ru/bacterial/core/search_id.php?id_list=23173>
glyco:is_glycan_database <http://purl.jp/bio/12/database/bcsdb>; dcterms:identifier “23173”.
<http://csdb.glycoscience.ru/bacterial/core/search_id.php?id_list=6920>
glyco:is_glycan_database <http://purl.jp/bio/12/database/bcsdb>; dcterms:identifier “6920”.
<http://www.genome.jp/dbget-bin/www_bget?carbbank+14848>
glyco:is_glycan_database <http://purl.jp/bio/12/database/ccsd>; dcterms:identifier “14848”.
<http://www.ebi.ac.uk/eurocarb/show_glycan.action?glycanSequenceId=2711>
glyco:is_glycan_database <http://purl.jp/bio/12/database/eurocarb-dbi>; dcterms:identifier “2711”.
 <http://www.glycosciences.de/sweetdb/start.php?action=explore_linucsid&linucsid=2611&show=1#struct%0A%20%20%09%09>
glyco:is_glycan_database <http://purl.jp/bio/12/database/glycosciences.de>;  dcterms:identifier “2611”.
<_:1>  glyco:is_glycan_database <someUUID> ; dcterms:identifier “123” .

<someUUID>
    glyco:url_template "http://foo.bar.com/someglycan?id=%s" ;
    glyco:abbreviation "foobar" ;
    glyco:category "glycan structure database" ;
    a glyco:glycan_database ;
    rdfs:label "FooBarDB" .
```

###List of existing Glycan databse URI's
These are URLs of databases that may be referenced. [?id?] placeholder for database internal id
<table>
  <tr><th>Database name</th><th>Description<th><th>URL template</th></tr>
  <tr><td>ccsd</td><td>Web link to a CarbBank entry about this carbohydrate. </td><td>http://www.genome.jp/dbget-bin/www_bget?carbbank+[?id?]</td></tr>
  <tr><td>glycomedb</td><td>Web link to a GlycomeDB entry about this carbohydrate.</td><td>http://www.glycome-db.org/database/showStructure.action?glycomeId=[?id?]</td></tr>
  <tr><td>jcggdb</td><td>Web link to a JCGGDB entry about this carbohydrate.</td><td>http://jcggdb.jp/idb/jcggdb/[?id?]</td></tr>
  <tr><td>kegg_glycan</td><td>Web link to a KEGG Glycan entry about this carbohydrate.</td><td>http://www.genome.jp/dbget-bin/www_bget?gl:[?id?]</td></tr>
  <tr><td>cfg</td><td>Web link to a CFG entry about this carbohydrate.</td><td>http://www.functionalglycomics.org/glycomics/CarbohydrateServlet?pageType=view&view=view&operationType=view&carbId=[?id?]&sideMenu=no%0A%20%20%09%09</td></tr>
  <tr><td>glyaffinity</td><td>Web link to a GlyAffinity entry about this carbohydrate.</td><td>http://worm.mpi-cbg.de/affinity/structure.action?ID=[?id?]</td></tr>
  <tr><td>glycobase_lille</td><td>Web link to a GlycoBase(Lille) entry about this carbohydrate.</td><td>http://glycobase.univ-lille1.fr/base/view_mol.php?id=[?id?]</td></tr>
  <tr><td>glycosciences.de</td><td>Web link to a GLYCOSCIENCES.de entry about this carbohydrate.</td><td>http://www.glycosciences.de/sweetdb/start.php?action=explore_linucsid&linucsid=[?id?]&show=1#struct%0A%20%20%09%09</td></tr>
  <tr><td>PDB</td><td>Web link to a PDB entry about this carbohydrate.</td><td>http://www.rcsb.org/pdb/explore/explore.do?structureId=[?id?]</td></tr>
  <tr><td>unicarbkb</td><td>Web link to a UniCarbKB entry about this carbohydrate.</td><td>http://unicarbkb.org/structure/:[?id?]</td></tr>
  <tr><td>bcsdb</td><td>Web link to a BCSDB entry about this carbohydrate.</td><td>http://csdb.glycoscience.ru/bacterial/core/search_id.php?id_list=[?id?]</td></tr>
  <tr><td>glyco</td><td></td><td></td></tr>
  <tr><td>glycobase_dublin</td><td>(Registration is required)</td><td></td></tr>
  <tr><td>unicarbdb</td><td>Web link to a UniCarb-DB entry about this carbohydrate.</td><td>http://unicarb-db.biomedicine.gu.se/unicarbdb/show_glycan.action?glycanSequenceId=[?id?]</td></tr>
  <tr><td>eurocarbdb-ebi</td><td>Web link to a EuroCarbDB (EBI) entry about this carbohydrate.</td><td>http://www.ebi.ac.uk/eurocarb/show_glycan.action?glycanSequenceId=[?id?]</td></tr>
  <tr><td>eurocarbdb-nibrt</td><td><td><td></td></tr>
</table>

databases of  glycan database https://docs.google.com/document/d/1xy3N7Njsm0EO9fjjp3GC-wuDG3TPcUGQnGPdltp0YpI/edit



#Images
The following table contains information about links to graphical representations of the carbohydrate.

##Table 9. Describing an image representation of a Glycan.

<table>
  <tr><th>predicate</th>		<th>data type</th>	<th>comment</th></tr>
  <tr><td>has_image</td><td>Resource</td><td>URL of image</td></tr>
  <tr><td>dc:format</td><td>xsd:String</td><td>The file format of the image. (image/svg+xml, image/png, image/gif, …)</td></tr>
  <tr><td>symbol_format</td><td>xsd:String or Resource</td><td>URL to explanation of symbol? The display style of the glycan. (cfg, uoxf, atoms)</td></tr>
</table>

```
Turtle example:
@prefix glycoSequence:  <http://purl.jp/bio/12//glycanSequence/0.1/> .
@prefix glyco:   <http://www.glycome-db.org/rdf/2012/glyco/1.0#> .

<http://www.glycome-db.org/rdf/3018>
      glyco:has_image <http://www.glycome-db.org/http-services/getImage.action?suspress=yes&id=3018>;
<http://www.glycome-db.org/http-services/getImage.action?suspress=yes&id=3018>
              dc:format       "image/png" ;
              glyco:symbol_format "cfg".
```            

#Compositions
<table>
  <tr><th>predicate</th>		<th>data type</th>	<th>comment</th></tr>
  <tr><td>has_component</td>	<td>Resource</td>	<td>Reference to another subject in the document describing a part of the composition in detail.</td></tr>
  <tr><td>has_cardinality</td>	<td>xsd:Integer</td>	<td>Number of occurrences of an element (e.g. a monosaccharide) in the subject. This information can be missing in case the cardinality cannot be defined (e.g. repeat units with unknown or under-defined repeats). Missing for non-stoichiometrical residues.</td></tr>
  <tr><td>has_cardinality_per_repeat</td>	<td>xsd:Integer</td>	<td>Number of occurrences of an element (e.g. a monosaccharide) in the repeat unit. Applicable to repeatUnits only. Missing for non-stoichiometrical residues.</td></tr>
  <tr><td>has_monosaccharide</td>	<td>Resource</td><td>Reference to a RDF resource describing the monosaccharide.</td></tr>
</table>

Example stucture:

Turtle example:
```
@prefix glycoSequence:  <http://purl.jp/bio/12//glycanSequence/0.1/> .
@prefix glyco:   <http://www.glycome-db.org/rdf/2012/glyco/1.0#> .

<http://www.glycome-db.org/rdf/2015>
      glyco:has_component
              [ glyco:has_cardinality      "1" ;				#this is only applicable to oligomers
                glyco:has_monosaccharide
                        "http://www.monosaccharidedb.org/query_monosaccharide_by_name.action?scheme=msdb&name=x-dglc-HEX-x:x||(2d:1)n-acetyl"
              ] ;
      glyco:has_component
              [ glyco:has_cardinality
                        "2" ;
                glyco:has_monosaccharide
                        "http://www.monosaccharidedb.org/query_monosaccharide_by_name.action?scheme=msdb&name=a-lgal-HEX-1:5|6:d"
              ] ;
      glyco:has_component
              [ glyco:has_cardinality
                        "1" ;
                glyco:has_monosaccharide
                        "http://www.monosaccharidedb.org/query_monosaccharide_by_name.action?scheme=msdb&name=b-dgal-HEX-1:5"
              ] .
```

# Biological source

see Source RDF in:
 https://docs.google.com/document/d/1rLJWha_5oXWGgPq8VhytTzJk1grkizVYtWQ7XXOBoXk/edit


# Publication references

see Publication RDF in:
 https://docs.google.com/document/d/1rLJWha_5oXWGgPq8VhytTzJk1grkizVYtWQ7XXOBoXk/edit


# Experimental data
see Evidence RDF in:
 https://docs.google.com/document/d/1rLJWha_5oXWGgPq8VhytTzJk1grkizVYtWQ7XXOBoXk/edit

Glyco relationship RDF
Glyco relationship RDF links glycan structure, biological source, publication and experimental data.

https://docs.google.com/document/d/1rLJWha_5oXWGgPq8VhytTzJk1grkizVYtWQ7XXOBoXk/edit

# Monosaccharide information
Thomas: The following table contains the RDF properties for single monosaccharides.
name

<table>
  <tr><th>predicate</th>		<th>data type</th>	<th>comment</th></tr>
  <tr><td>name</td>			<td>xsd:String</td>	<td>MsDB name of the monosaccharide</td></tr>
  <tr><td>has_basetype</td>		<td>Resource</td>	<td>reference to another RDF resource with URI describing the monosaccharide basetype</td></tr>
  <tr><td>has_substituent</td>		<td>Resource</td>	<td>reference to another RDF resource with URI. The substituent is linked to the basetype in this monosaccharide.</td></tr>
  <tr><td>average_MW</td>		<td>xsd:double</td>	<td>literal numeric with decimal, calculated from monosaccharide composition with average atomic weight</td></tr>
  <tr><td>monoisotopic_MW</td>		<td>xsd:double</td>	<td>literal numberic with decimal, calculated from monosaccharide composition with atomic weight of monoisotope.</td></tr>
  <tr><td>has_linking_position</td>	<td>xsd:integer</td>	<td>monosaccharide can be linked to other residues via standard glycosidic linkage at the given backbone position</td></tr>
  <tr><td>has_alias_name</td>		<td>Resource?</td><td>[scheme:String; name:String; external_substituent[name; position; linkage_type]; is_primary] name of the monosaccharide in a given notation scheme (external substituents only apply to specific residues / schemes) The following table contains the RDF properties for monosaccharide basetypes.</td></tr>
  <tr><td>size</td>			<td>xsd:integer</td>	<td>number of backbone carbon atoms</td></tr>
  <tr><td>average_MW</td>		<td>xsd:double</td>	<td>literal numeric with decimal, calculated from monosaccharide composition with average atomic weight</td></tr>
  <tr><td>monoisotopic_MW</td>		<td>xsd:doubel</td>	<td>literal numberic with decimal, calculated from monosaccharide composition with atomic weight of monoisotope.</td></tr>
  <tr><td>anomeric</td>			<td>Resource</td>	<td>alpha, beta, none, unknown (URI for concept to be provided). anomeric state of the basetype</td></tr>
  <tr><td>configuration</td>		<td>Resource</td>	<td>D, L, unknown, none (URI for concept to be provided. absolute configuration of the basetype</td></tr>
  <tr><td>ring_start</td>		<td>xsd:integer</td>	<td>position of first carbon involved in ring closure</td></tr>
  <tr><td>ring_end</td>			<td>xsd:integer</td>	<td>position of second carbon involved in ring closure</td></tr>
  <tr><td>stereocode</td>		<td>xsd:String</td>	<td>Stereocode describing the backbone stereochemistry</td></tr>
  <tr><td>ext_stereocode</td>		<td>xsd:String</td>	<td>Extended stereocode of the basetype</td></tr>
  <tr><td>has_composition</td>		<td></td><td></td></tr>
  <tr><td>has_core_modification</td>	<td>Resource</td>	<td>reference to another RDF describing a core modification that is present in this basetype</td></tr>
</table>

# Other Glycan information

<table>
  <tr><th>predicate</th>		<th>data type</th>	<th>comment</th></tr>
  <tr><td>has_standard_MW</td>	<td>xsd:double</td>	<td>literal numeric with decimal, calculated from monosaccharide composition with standard atomic weight (
http://physics.nist.gov/cgi-bin/Compositions/stand_alone.pl?ele=&ascii=html&isotype=some )</td></tr>
  <tr><td>has_monoisotopic_MW</td><td>xsd:double</td>	<td>literal numeric with decimal, calculated from monosaccharide composition with atomic weight of monoisotope.</td></tr>
</table>

# Glycan Function
<table>
  <tr><th>predicate</th>		<th>data type</th>	<th>comment</th></tr>
  <tr><td>has_motif</td>		<td>Resource</td>	<td>reference to another RDF resource with URI. The object is a structurally defined motif
Eg. for Neo-lacto motif
http://jcggdb.jp/idb/motif?id=JCGG-MOTIF3009.rdf
inverse of ”contained_in”.
should have sequence, composition, image ...</td></tr>
  <tr><td>has_epitope</td>		<td>Resource</td>	<td>reference to another RDF resource with URI. The subject is a structural motif  with biological relevance; subclass of has_motif.</td></tr>
  <tr><td>contained_in</td>		<td>Resource</td>	<td>reference to another RDF resource with URI. The subject is a structurally defined motif, and the object is a glycan structure or motif.</td></tr>
  <tr><td>has_affinity_to</td>		<td>Resource</td>	<td>Subject is a material or organism, which has affinity to  the object. </td></tr>
  <tr><td>degraded_by</td>		<td>Resource</td>	<td>Subject is an enzyme, which degrades the object.</td></tr>
  <tr><td>generated_by</td>		<td>Resource</td>	<td>Subject is an enzyme, which synthesize the object.</td></tr>
  <tr><td>degraded_from</td>		<td>Resource</td>	<td>Subject is a precursor of the term “degraded_by”</td></tr>
  <tr><td>generated_from</td>		<td>Resource</td>	<td>Subject is a precursor of the term “generated_by”</td></tr>
</table>

Turtle example:
```
@prefix glycoSequence:  <http://purl.jp/bio/12//glycanSequence/0.1/> .
@prefix glyco:   <http://www.glycome-db.org/rdf/2012/glyco/1.0#> .

<http://www.glycome-db.org/rdf/2015>
...
```

#Namespace or Vocabularies for Describing GlycoProtein

```
prefix, uniprotcore:http://purl.uniprot.org/core/
```

https://docs.google.com/spreadsheet/ccc?key=0Ajw2OqykvyGLdG9FOHN4ZENYZmpVVkhCYmZFc3dwX3c#gid=2

<table>
  <tr><th>predicate</th>		<th>data type</th>	<th>comment</th></tr>
  <tr><td>rdf:type</td>			<td>Resource</td>	<td>Description</td></tr>
  <tr><td>has_core_protein</td>		<td>uniprotcore:Protein</td> 	<td>Uniprot identifier for glycoprotein entry</td></tr>
  <tr><td>amino_acid_length</td>	<td></td> 	<td>From relevant uniprot page or stated if sequenced/synthesised</td></tr>
  <tr><td>amino_acid_sequence</td>	<td></td>	<td></td></tr>
  <tr><td>versionOf</td>		<td></td>	<td></td></tr>
  <tr><td>has_glycosylated_amino_acid_residue</td>	<td>Resource</td>	<td>use UUID if URI not available</td></tr>
  <tr><td>position_of_amino_acid</td>	<td>xsd:int</td>	<td>property of “has_glycosylated_amino_acid_residue”, Amino acid position</td></tr>
  <tr><td>amino_acid_type</td>		<td>Resource</td>	<td>Link to definition of amino acid residue. property of “has_glycosylated_amino_acid_residue”, type of amino acid residue, usually N or S/T</td></tr>
  <tr><td>modification_type</td>	<td>Resource</td>	<td>property of “has_glycosylated_amino_acid_residue” The object is referenced to list below.</td>
  <tr><td>has_structure</td>		<td>Resouce</td>	<td>URI of structure associated with glycoprotein (predicate can occur multiple times)</td>
  <tr><td>evidence</td></tr>
  <tr><td>contributor</td></tr>
</table>


```
<http://unicarbkb.org/protein/Q8TAX7> a glyco:glycosylation_annotation;
glyco:has_uniprot <http://uniprot.org/Q8TAX7>;
glyco:has_glycosylated_amino_acid_residue “”,   
	glyco:has_structure <http://unicarbkb.org/structure/5989> .  (contain many structures, which can be linked to site via BNode)
```
