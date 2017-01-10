TEI ENCODING OF THE DASG FIELDWORK ARCHIVE
------------------------------------------

The top-level file in the fieldwork archive is:

> FieldworkArchive.xml

This file is a TEI corpus with the following structure:

<teiCorpus xml:lang="gd">
  <teiHeader>
    <fileDesc>
      <titleStmt>
        <title xml:lang="gd">Dachaigh airson Storas na Gàidhlig: Faclan bhon t-Sluagh</title>
      </titleStmt>
      <publicationStmt>
        <p/>
      </publicationStmt>
      <sourceDesc>
        <p/>
      </sourceDesc>
    </fileDesc>
  </teiHeader>
  <TEI xml:id="...">...</TEI>
  <TEI xml:id="...">...</TEI>
  <TEI xml:id="...">...</TEI>
  ...
</teiCorpus>

Note: 

1. The default language of the corpus as a whole is Gaelic. Any elements containing English text will need to be specified as such.

2. Every individual questionnaire and wordlist is encoded as a TEI element, with a unique ID. 

3. These IDs are typically constructed on the pattern BOX_PLACE+PERSON+TOPIC, e.g. "HarrisVarious_HarrisSgarastamhorAMacLennanlobster".

4. Rather than have every questionaire/wordlist encoded directly in the FieldworkArchive.xml, there is one actually file for each, e.g. HarrisSgarastamhorAMacLennanlobster.xml.

5. XInclude is used in the FieldworkArchive.xml file to link to these files, e.g. <xi:include href="AberfeldyPStewartslips.xml"/>.

----------

There are two very important TEI files which are not encodings of questionnaires or wordlists:

> list_of_people.xml

> list_of_places.xml

The first of these contains a complete list of all of the people involved in creating the fieldwork archive: informants, fieldworkers, editors, etc.
This file has the following structure:

<TEI xml:id="list_of_people">
  <teiHeader>...</teiHeader>
  <text>
    <body>
      <listPerson>
        <person xml:id="A_MacLennan_Harris_Gobhaig">...</person>
        <person xml:id="Donald_MacLennan_Harris_Govaig">...</person>
        ...
      </listPerson>
    </body>
  </text>
</TEI>

Note that every person has a unique ID, usually formed as NAME_PLACE.

The full structure of the 'person' elements is as follows:

<person xml:id="Donald_MacDonald_Harris_Horgabost">
  <persName xml:lang="en">
    <forename>Donald</forename>
    <surname>MacDonald</surname>
  </persName>
  <persName>
    <forename>Domhnall</forename>
    <surname>Domhnallach</surname>
  </persName>
  <age>62</age>
  <birth>
    <location corresp="Harris_Horgabost"/>
  </birth>
</person>

Note that the birth>location element is used to encode the 'informant origin' field from the questionaires and wordlists. 
The 'corresp' attribute is an IDREF that must point to a valid 'place' element in the file 'list_of_places.xml' (see next).

The second file, 'list_of_places.xml', contains a complete, hierarchical list of all of the places involved in creating the fieldwork archive.
It has the following structure:

<TEI xml:id="list_of_places">
  <teiHeader>...</teiHeader>
  <text>
    <body>
      <listPlace>
        <place xml:id="Harris">
          ...
          <place xml:id="North_Harris">
            ...
            <place xml:id="Harris_Gobhaig">...</place>
            <place xml:id="Harris_Ardhasaig">...</place>
            ...
          </place>
          ...
        </place>
        <place xml:id="Lewis">...</place>
        ...
     </listPlace>
    </body>
  </text>
</TEI>

Note that where a place is located WITHIN another, bigger place, then this is refelected directly by embedding 'place' elements within each other.

Places can also have names and locations (using standard GPS coordinates).

<place xml:id="Harris_Leverburgh">
  <placeName xml:lang="en">Leverburgh</placeName>
  <placeName>An t-Òb</placeName>
  <location>
    <geo>57.817662 -6.968475</geo>
  </location>
</place>

----------

The questionnaires and wordlists are encoded as TEI elements, with the following structure:

<TEI xml:id="HarrisVarious_HarrisSgarastamhorAMacLennanlobster">
  <teiHeader>
    <fileDesc>
      <titleStmt>
        <title/>
      </titleStmt>
      <publicationStmt>
        <p/>
      </publicationStmt>
      <notesStmt>
        <note>...</note>
        <note>...</note>
      </notesStmt>
      <sourceDesc>
        <p/>
      </sourceDesc>
    </fileDesc>
    <profileDesc>
      <creation>
        <location corresp="Harris_Sgarastamhor"/>
        <date>??</date>
      </creation>
      <particDesc>
        <person role="fieldworker" corresp="anonymous_D"/>
        <person role="informant" corresp="Angus_MacLennan_Harris_Sgarastamhor"/>
      </particDesc>
      <textClass>
        <keywords>
          <term xml:lang="en">Lobster-Fishing</term>
          <term>Iasgach a’ Ghiomaich</term>
        </keywords>
      </textClass>
    </profileDesc>
  </teiHeader>
  <text>
    <body>...</body>
  </text>  
</TEI>

Note:

1. The 'corresp' attribute within creation>location is an IDREF which must point to a valid 'place' in the file 'list_of_places.xml'.

2. The 'corresp' attributes within particDesc>person are IDREFs which must point to a valid 'person' in the file 'list_of_people.xml'.

3. Where a question mark is used in the original to indicate uncertainty, use the attribute cert="medium", e.g.

<person role="fieldworker" corresp="A_J_Smith" cert="medium"/>


The 'body' of each document is typically a sequence of 'entry' elements:

<body>
  <entry xml:id="HarrisVarious_HarrisSgarastamhorAMacLennanlobster-d0e31">...</entry>
  <entry xml:id="HarrisVarious_HarrisSgarastamhorAMacLennanlobster-d0e40">...</entry>
  ...
</body>

Note that every 'entry' has a unique ID, formed on the pattern FILEID-XXX, where XXX is a random sequence of letters and digits.

Entries can be interspersed with 'note' elements, and also 'figure>graphic' elements pointing to illustrations:

<body>
  ...
  <entry>...</entry>
  <note>...</note>
  <entry>...</entry>
  ...
  <entry>...</entry>
  <figure>
    <graphic url="..." width="...px"/>
  </figure>
  <entry>...</entry>
  ...
</body>

Where entries are organised into hierarchical sections, this is encoded using 'div' and 'head' elements, as follows:

<body>
  <div>
    <head>1 ...</head>
    <div>
      <head>A ...</head>
      <entry>...</entry>
      <entry>...</entry>
      ...
    </div>
    <div>
      <head>B ...</head>
      <entry>...</entry>
      <entry>...</entry>
      ...
    </div>
  </div>
  <div>
    <head>2 ...</head>
    <entry>...</entry>
    <entry>...</entry>
    ...
  </div>
</body>

For legacy reason, every 'head' element has a unique ID, similar to those for entries.

Individual entries have the following basic structure (though this needs further elaboration):

<entry xml:id="...">
  <form>
    <orth>...</orth>
    <pron>[...]</pron>
  </form>
  <def>...</def>
  <note>...</note>
  <note>...</note>
  ...
</entry>

Note:

1. form>orth contains the orthographic form of the headword

2. form>pron contains its pronunciation, as IPA

3. 'def' contains the definition, possibly including 'graphic' elements for illustrations

----------

Some advanced, experimental features (ignore for now):

<entry xml:id="HarrisMacLennan_HarrisGobhaigMacLennanbiadh-d0e43" corresp="lexicopia:bracaist">
  <form>
    <orth>
      <choice>
        <orig>braiceast</orig>
        <reg>bracaist</reg>
      </choice>
    </orth>
  </form>
</entry>

Note:

1. Where the form used in the original document is non-standard in some way, the 'choice' element can be used to represent a regularised form.

2. Entries can be linked to a gold standard entry ID in Lexicopia/GD using the 'corresp' attribute.




