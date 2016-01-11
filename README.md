![alt tag] (https://lh3.googleusercontent.com/lSPWRu9qbTLvs5wHHvYrBq7Ud_XZo5osbLmQioj4Yex799qEdLw7Tyr0L6J8vEYDMBxaRMqBsAIRfbkDGZOUp_v1EperUpH_o4Hm9wkzF7V4ySdNLEjJ3mmlYyg37FC6LFWl6_KKIqZqzMOe_YQgq-As8gPeWgaeQP4-799dzubOSYBDELHInYOjYYhgAls1d4xEUdO6sL4vcLjO1xDjKgXPMvbFntZbO5kwgbwNDZp5XhvhfNV1OuCmhojSru2ijv4Av4mGzHI3NN4sedr31S2RhPIrf2XquKfGUlZ2bdREE7GU-V0EUnboph9b4Seov1S4NS35IpGZz7TTa6I-uUwKJWHH2PR4Xuj2OJ-MHRtAsDlRBV7-WqRV1yqKM5Vm9kkXWOvmer81SX8IzBzwsf3Mf42hf3K3sOQOvrNP1BpewUuJwo1vbQWRNaXV7IKZwJT889kIWqmAbGWeveQIDPPpA7YlbgASL4Nb1e14h5T8vbQ3oxDfVxHHvl8hLCcYYkbzZq8Qbdj51fo-YV4l_aXrD05-tI6UVaEMWCPNXu_lsQsLfnOS-QzH5b7fWgLspUfo=w354-h75-no)

# DESCRIOPTION
The [resim.jar](https://github.com/parklize/resim/blob/master/resim.jar) file is an implementation of RESIM (REsource SIMilarity) measure. The measure is designed to calculate the semantic similarity between two resources in a Knowlege Graph (e.g., DBpedia, zhishi.me) with a SPARQL Endpoint. RESIM is presented in [1] and then it is improved in [2] and the summary of the measure is presented in [3].

## REQUIREMENT
* Java 1.7
* JENA 2.11.2

## EXAMPLE
	public static void main(String[] args) {
		
		// similarity measure settings
		List<String> additionalPropertyList = Arrays.asList(
				"<http://purl.org/dc/terms/subject>", 
				"<http://www.w3.org/2000/01/rdf-schema#subClassOf>", 
				"<http://www.w3.org/2004/02/skos/core#narrowerOf>", 
				"<http://www.w3.org/2004/02/skos/core#broaderOf>",
				"<http://www.w3.org/1999/02/22-rdf-syntax-ns#type>"
				);
		List<String> includePropertyList = Arrays.asList(
				"<http://purl.org/dc/terms/subject>", 
				"<http://www.w3.org/2000/01/rdf-schema#subClassOf>", 
				"<http://www.w3.org/2004/02/skos/core#narrower>", 
				"<http://www.w3.org/2004/02/skos/core#broader>",
				"<http://www.w3.org/1999/02/22-rdf-syntax-ns#type>"
				);
		List<String> excludePropertyList = Arrays.asList(
				"<http://dbpedia.org/ontology/wikiPageWikiLink>" 
				);
				
		// initialize similarity measure
		// param1: SPARQL Endpoint URL
		// param2: pattern for property - default: "http://dbpedia.org/ontology/
		// param3: include property list
		// param4: additional property list to pattern
		// param5: exclude property list
		ResourceSimilarityMeasure rsm = new ResourceSimilarityMeasure("http://dbpedia.org/sparql", null, null, additionalPropertyList, excludePropertyList);	
		
		System.out.println(rsm.getSimilarity("<http://dbpedia.org/resource/Drink>", "<http://dbpedia.org/resource/Mouth>", 2));
	}
	
* The ResourceSimilarityMeasure requires 5 parameters. The first one is a SPARQL Endpoint (e.g., DBpedia SPARQL Endpoint) and the other ones are used for controling the property list for this measure. 
* The 2nd parameter (pattern) is used with 4th, 5th parameters. For example, the default pattern of property for this measure is "http://dbpedia.org/ontology/" (i.e., DBpedia Ontology properties) and it will consider/exclude the list of properties if there is an additional property list or an exclude property list exist.
* The 3rd parameter is an include property list that controls property list for this measure in a strict way. That is, the measure will only consider this property list if you define the list. 
	
## REFENRECES
1. Computing the Semantic Similarity of Resources in DBpedia for Recommendation Purposes, 
   Guangyuan Piao, Safina showkat Ara, John G. Breslin 5th Joint International Semantic Technology Conference, Yichang, China, 2015
2. Measuring Semantic Similarity for Linked Open Data-enabled Recommender Systems, Guangyuan Piao and John G. Breslin, The 31st             ACM/SIGAPP Symposium on Applied Computing, Pisa, Italy, 2016
3. Exploiting the Semantic Similarity of Interests in a Semantic Interest Graph for Social Recommendations, Guangyuan Piao, The 31st        ACM/SIGAPP Symposium on Applied Computing, Pisa, Italy, 2016
