# Spring - REST API

```java
@RestController
public class PlaceController {

	 private static final Logger logger = LoggerFactory.getLogger(PlaceController.class);
	
	// Add Place
	@PostMapping("places")
	public void addPlace(@RequestBody Place place) {
		logger.info("Add Place");
	}
	
  //Get All Places
	@GetMapping("places")
	public List<String> getAllPlaces() {
		logger.info("List Place");		
		List<String> places = List.of("Marina Beach", "Kalpakkam Beach");
		//Gson gson = new Gson();
		//String json = gson.toJson(places)
		//return json
		return places;
		
	}
	// Search by placeName
	@GetMapping("places/search")
	public List<String> searchPlace(@RequestParam("placeName") String placeName) {
    
		logger.debug("Search Place: {}" , placeName);		
    		logger.debug("Search Place:" + placeName);      
		List<String> places = List.of("Marina Beach", "Kalpakkam Beach");				  
		List<String> results = places.stream().filter(p-> p.contains(placeName)).collect(Collectors.toList());				
		return results;
		
	}
	
  //Get Place Details by Id
	@GetMapping("places/{id}")
	public Place getPlace(@PathVariable("id") Integer id) {				
    		logger.info("Get Place" + id);  
    		Place place = new Place("Marina Beach");  //return dummy place object
    		return place; 
	}
  
	//Update
	@PutMapping("places/{id}")
	public void updatePlace(@PathVariable("id") Integer id, @RequestBody Place place) {
		logger.info("Update Place");
	}
  
  
	//Partial Update
	@PatchMapping("places/{id}")
	public void updatePlace(@PathVariable("id") Integer id, @RequestBody Place place) {
		logger.info("Update Place City");
	}
	
	//Delete
	// http://localhost:8090/places/5
	// http://localhost:8090/places/4
	@DeleteMapping("places/{id}")
	public Integer deletePlace(@PathVariable("id") Integer id) {
		logger.info("Delete Place" + id);
		return id;
	}
	
	
}

```
