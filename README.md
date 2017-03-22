# DESCRIPTION
The [RESIM.jar](https://github.com/parklize/resim/blob/master/RESIM.jar) file is an implementation of RESIM (REsource SIMilarity) measure. The measure is designed to calculate the semantic similarity between two resources in a Knowlege Graph (e.g., DBpedia, Wikidata, zhishi.me) with a SPARQL Endpoint. RESIM is presented in [1] at first, and then it has been improved in [2]. The summary of the measure is presented in [3]. The implementation extends the measure further by enabling different properties for two resources, e.g., for incoming indirect link between dbpedia:Steve_Jobs and dbpedia:Apple_Inc., it can be connected by dbpedia:Steve_Jobs<-dbpedia-owl:keyPerson<-dbpedia:NexT->dbpedia-owl:successor->dbpedia:Apple_Inc. while in the paper we restrict the property should be the same. 

When writing a paper or producing a software application, tool, or interface based on the library, please kindly cite the source [2].

## REQUIREMENT
* Java 1.7
* JENA 2.11.2

Simply add jena files as well as RESIM.jar file in your building path to start.

![alt tag](https://github.com/parklize/resim/blob/master/path.png)

## EXAMPLE 1
The example shows using RESIM to calculate the similarity between HongKong and Singapore Wikidata entities. inbound and outbound properties are given based on your selected domain (e.g., Music). This example use predefined "prefixList" for SPARQL.

	public static void main(String[] args) {

		// Wikidata settings - must use prefix format
		ResourceSimilarityMeasure rsmForWikidata = new ResourceSimilarityMeasure( 
							PropertyRestriction.SamePropertyPath,
							"https://query.wikidata.org/sparql", 
							prefixList, null, 
							includeInboundPropertyList_wikidata, 
							includeOutboundPropertyList_wikidata, 
							null, null);
		
		// print similarity between HongKong and Singapore
		System.out.println(rsmForWikidata.getSimilarity("wd:Q8646", "wd:Q334", 2));
	}
	
	// prefix list
	final static String prefixList = "PREFIX wdt: <http://www.wikidata.org/prop/direct/>\n" 
            				+ "PREFIX wd: <http://www.wikidata.org/entity/>\n";
	
	// outbound properties used for consideration
	final static List<String> includeOutboundPropertyList_wikidata = Arrays.asList(
			"wdt:P31",
			"wdt:P17",
			"wdt:P131",
			"wdt:P190",
			"wdt:P910",
			"wdt:P47",
			"wdt:P1376",
			"wdt:P1464",
			"wdt:P1792",
			"wdt:P1465",
			"wdt:P150",
			"wdt:P421",
			"wdt:P1343",
			"wdt:P361",
			"wdt:P163",
			"wdt:P6"
			);
	
	// inbound properties used for consideration
	final static List<String> includeInboundPropertyList_wikidata = Arrays.asList(
			"wdt:P19",
			"wdt:P20",
			"wdt:P131",
			"wdt:P937",
			"wdt:P159",
			"wdt:P276",
			"wdt:P190",
			"wdt:P740",
			"wdt:P840",
			"wdt:P971",
			"wdt:P301",
			"wdt:P915",
			"wdt:P551",
			"wdt:P36",
			"wdt:P47",
			"wdt:P1408",
			"wdt:P931",
			"wdt:P291",
			"wdt:P150",
			"wdt:P17",
			"wdt:P706",
			"wdt:P138",
			"wdt:P1071",
			"wdt:P921",
			"wdt:P27",
			"wdt:P1001",
			"wdt:P127",
			"wdt:P180",
			"wdt:P504",
			"wdt:P1427",
			"wdt:P119",
			"wdt:P1444",
			"wdt:P495"
			);

## EXAMPLE 2
The example shows using RESIM to calculate the similarity between HongKong and Singapore DBpedia entities. inbound and outbound properties are given based on your selected domain (e.g., Music). This example shows without prefix list for SPARQL.

	public static void main(String[] args) {
		
		// DBpedia settings - without prefix list format
		ResourceSimilarityMeasure rsmForDBpedia = new ResourceSimilarityMeasure(
							PropertyRestriction.SamePropertyPath,
							"http://dbpedia.org/sparql", 
							null, null, 
							includeInboundPropertyList_dbpedia, 
							includeOutboundPropertyList_dbpedia, 
							null, null);	
		
		System.out.println(
		rsmForDBpedia.getSimilarity("<http://dbpedia.org/resource/Hong_Kong>", "<http://dbpedia.org/resource/Singapore>", 2));
	
	}
	
	// DBpeida outbound properties
	final static List<String> includeOutboundPropertyList_dbpedia = Arrays.asList(
			"<http://purl.org/dc/terms/subject>",
			"<http://www.w3.org/1999/02/22-rdf-syntax-ns#type>",
			"<http://dbpedia.org/ontology/isPartOf>",
			"<http://dbpedia.org/ontology/country>",
			"<http://dbpedia.org/ontology/timeZone>",
			"<http://dbpedia.org/ontology/type>",
			"<http://dbpedia.org/ontology/region>",
			"<http://dbpedia.org/ontology/province>",
			"<http://dbpedia.org/ontology/leaderName>",
			"<http://dbpedia.org/ontology/saint>",
			"<http://dbpedia.org/ontology/neighboringMunicipality>",
			"<http://dbpedia.org/ontology/district>",
			"<http://dbpedia.org/ontology/governmentType>",
			"<http://dbpedia.org/ontology/daylightSavingTimeZone>",
			"<http://dbpedia.org/ontology/frazioni>",
			"<http://dbpedia.org/ontology/state>",
			"<http://dbpedia.org/ontology/leaderParty>",
			"<http://dbpedia.org/ontology/part>",
			"<http://dbpedia.org/ontology/twinCity>"
			);
		
	// DBpeida inbound properties
	final static List<String> includeInboundPropertyList_dbpedia = Arrays.asList(
			"<http://dbpedia.org/ontology/birthPlace>",
			"<http://dbpedia.org/ontology/location>",
			"<http://dbpedia.org/ontology/deathPlace>",
			"<http://dbpedia.org/ontology/city>",
			"<http://dbpedia.org/ontology/hometown>",
			"<http://dbpedia.org/ontology/recordedIn>",
			"<http://dbpedia.org/ontology/residence>",
			"<http://dbpedia.org/ontology/isPartOf>",
			"<http://dbpedia.org/ontology/headquarter>",
			"<http://dbpedia.org/ontology/locationCity>",
			"<http://dbpedia.org/ontology/routeJunction>",
			"<http://dbpedia.org/ontology/broadcastArea>",
			"<http://dbpedia.org/ontology/builder>",
			"<http://dbpedia.org/ontology/routeStart>",
			"<http://dbpedia.org/ontology/nearestCity>",
			"<http://dbpedia.org/ontology/routeEnd>",
			"<http://dbpedia.org/ontology/ground>",
			"<http://dbpedia.org/ontology/foundationPlace>",
			"<http://dbpedia.org/ontology/assembly>",
			"<http://dbpedia.org/ontology/restingPlace>",
			"<http://dbpedia.org/ontology/place>",
			"<http://dbpedia.org/ontology/district>",
			"<http://dbpedia.org/ontology/countySeat>",
			"<http://dbpedia.org/ontology/locatedInArea>",
			"<http://dbpedia.org/ontology/country>",
			"<http://dbpedia.org/ontology/capital>",
			"<http://dbpedia.org/ontology/region>",
			"<http://dbpedia.org/ontology/populationPlace>",
			"<http://dbpedia.org/ontology/neighboringMunicipality>",
			"<http://dbpedia.org/ontology/largestCity>",
			"<http://dbpedia.org/ontology/type>",
			"<http://dbpedia.org/ontology/garrison>",
			"<http://dbpedia.org/ontology/owner>",
			"<http://dbpedia.org/ontology/homeport>",
			"<http://dbpedia.org/ontology/part>",
			"<http://dbpedia.org/ontology/regionServed>",
			"<http://dbpedia.org/ontology/team>",
			"<http://dbpedia.org/ontology/mouthMountain>",
			"<http://dbpedia.org/ontology/mouthPlace>",
			"<http://dbpedia.org/ontology/billed>",
			"<http://dbpedia.org/ontology/campus>",
			"<http://dbpedia.org/ontology/arrondissement>",
			"<http://dbpedia.org/ontology/origin>",
			"<http://dbpedia.org/ontology/county>",
			"<http://dbpedia.org/ontology/almaMater>",
			"<http://dbpedia.org/ontology/metropolitanBorough>",
			"<http://dbpedia.org/ontology/education>",
			"<http://dbpedia.org/ontology/premierePlace>",
			"<http://dbpedia.org/ontology/training>",
			"<http://dbpedia.org/ontology/state>",
			"<http://dbpedia.org/ontology/picture>",
			"<http://dbpedia.org/ontology/localAuthority>",
			"<http://dbpedia.org/ontology/majorShrine>",
			"<http://dbpedia.org/ontology/twinCity>",
			"<http://dbpedia.org/ontology/highschool>",
			"<http://dbpedia.org/ontology/municipality>",
			"<http://dbpedia.org/ontology/operator>",
			"<http://dbpedia.org/ontology/spokenIn>",
			"<http://dbpedia.org/ontology/locationCountry>",
			"<http://dbpedia.org/ontology/administrativeDistrict>",
			"<http://dbpedia.org/ontology/nationality>",
			"<http://dbpedia.org/ontology/sourcePlace>"
			);
		
	
## EXAMPLE 3
	public static void main(String[] args) {
		
		// DBpedia settings - without giving prefix list, using property patterns instead
		// it will filter properties which start with ""http://dbpedia.org/ontology"
		ResourceSimilarityMeasure rsmForDBpedia = new ResourceSimilarityMeasure(PropertyRestriction.SamePropertyPath,
							     "http://dbpedia.org/sparql", null, "http://dbpedia.org/ontology/", 
							     null, null, null, null);	
		System.out.println(
		rsmForDBpedia.getSimilarity("<http://dbpedia.org/resource/Hong_Kong>", "<http://dbpedia.org/resource/Singapore>", 2));
		
	}
	
## PARAMETERS
* P1: Use one of "PropertyRestriction.SamePropertyPath" or "PropertyRestriction.DifferentPropertyPath", "SamePropertyPath" denotes considering paths with the same propery, e.g., Hong_Kong->p1->?<-p1<-Singapore, Hong_Kong<-p1<-?->p1->Singapore. On the other hand, "DifferentPropertyPath" denotes considering paths with the differnt/same propery, e.g., Hong_Kong->p2->?<-p1<-Singapore, Hong_Kong<-p2<-?->p1->Singapore.
* P2: SPARQL Endpoint
* P3: String for prefix list if any
* P4: Property filtering pattern (See Example 3)
* P5: Inbound property list
* P6: Outbound property list
* P7: Additional property list. This can be used with P4. For example, after defining property filtering pattern, e.g., "http://dbpedia.org/ontology/", and you can define this list (e.g., "http://purl.org/dc/terms/subject") to add more properties for consideration.
* P8: Exclude property list. Similary to P7, define the list to exclude some properties from defined property filtering pattern.
	
## REFENRECES
1. Computing the Semantic Similarity of Resources in DBpedia for Recommendation Purposes, 
   Guangyuan Piao, Safina showkat Ara, John G. Breslin 5th Joint International Semantic Technology Conference, Yichang, China, 2015 [[PDF]](https://www.researchgate.net/publication/298070195_Computing_the_Semantic_Similarity_of_Resources_in_DBpedia_for_Recommendation_Purposes)
2. Measuring Semantic Similarity for Linked Open Data-enabled Recommender Systems, Guangyuan Piao and John G. Breslin, The 31st             ACM/SIGAPP Symposium on Applied Computing, Pisa, Italy, 2016 [[PDF]](https://www.researchgate.net/publication/298070201_Measuring_Semantic_Distance_for_Linked_Open_Data-enabled_Recommender_Systems)
3. Exploiting the Semantic Similarity of Interests in a Semantic Interest Graph for Social Recommendations, Guangyuan Piao, The 31st        ACM/SIGAPP Symposium on Applied Computing, Pisa, Italy, 2016
