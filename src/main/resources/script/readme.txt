First of all you must go to http://www.mockaroo.com/ and register there. Then you create new schema. The first schema is 'address'. There are such filds, its types and options:

-------------------------------------------
| Field Name | 	     Type       | Options |
-------------------------------------------
| _id	     | MongoDB ObjectID | none	  |
| country    | Country		| none	  |
| city       | City		| none    |
| street     | Street Name	| none	  |
| building   | Street Number	| none    |
-------------------------------------------

After that you can choose amount of rows and set JSON format. Then you need to click on the button 'Download Data'.
Further you must create new java project and copy json-file to project folder. Then you need to run following script:

public static void main(String[] args) throws IOException {
	BufferedReader br = new BufferedReader(new FileReader("address.json"));
	try {
		StringBuilder sb = new StringBuilder();
		String line = br.readLine();

		while (line != null) {
			sb.append(line);
			sb.append(System.lineSeparator());
			line = br.readLine();
		}
		String everything = sb.toString();
		String updated = everything.replace("{\"$oid\":", "ObjectId(");
		String updated2 = updated.replace("\"},\"", "\"),\"");
		System.out.println("db.address.insertMany(" + updated2 + ")");
	} finally {
		br.close();
	}
}

This script changes source json-text to the format that you need. After this action you need to create js-file, enter the command 'db = db.getSiblingDB('hotel_db')' and copy text from eclipse console to this file.

The next step is adding 'address' schema to the datasets in http://www.mockaroo.com/. For this step you need to click on 'DATASETS' in menu. Than click on 'Upload a New Dataset', enter a name and choose the file. But the file must be .csv. You can convert json to csv by online converter, for example, https://json-csv.com/, https://konklone.io/json/ etc.

The next schema is 'hotel'. There are such filds, its types and options:
---------------------------------------------------------------------------------------------------------
| Field Name 	          | Type 	      | Options 						|
---------------------------------------------------------------------------------------------------------
| _id	     	          | MongoDB ObjectID  | none							|
| address_id 	    	  | Dataset Column    | address, _id_$oid, random				|
| name                    | Fake Company Name | none							|
| phone    	          | Phone	      | format: ###-###-####					|
| aditional_service[8-10] | Custom List	      | Parking, Swimming Pool, WiFi, Outdoor Pool, 		|
|			  |		      | Non-smoking Rooms, Pet Friendly, Family Rooms, Bar, 	|
|			  |		      | Airport Shuttle, TV, Air conditioning, Phone,  		|
|			  |		      | Elevator, Spa, Laundry, 24-Hour Front Desk, Restaurant, |
|			  |		      | Fitness Center, Room Service, Facilities for Disabled 	|
|			  |		      | Guests; Distribution Type: random			|
---------------------------------------------------------------------------------------------------------

After that you can choose amount of rows and set JSON format. Then you need to click on the button 'Download Data'.
Further you must copy json-file to java project folder. Then you need to run following script:

public static void main(String[] args) throws IOException {
	BufferedReader br = new BufferedReader(new FileReader("hotel.json"));
	try {
		StringBuilder sb = new StringBuilder();
		String line = br.readLine();

		while (line != null) {
			sb.append(line);
			sb.append(System.lineSeparator());
			line = br.readLine();
		}
		String everything = sb.toString();
		String updated = everything.replace("{\"$oid\":", "ObjectId(");
		String updated2 = updated.replace("address_id\":\"", "address_id\":ObjectId(\"");
		String updated3 = updated2.replace("\",\"name", "\"),\"name");
		String updated4 = updated3.replace("\"},\"", "\"),\"");
		System.out.println("db.hotel.insertMany(" + updated4 + ")");
	} finally {
		br.close();
	}
}

After this action you need to copy text from eclipse console to js-file that you created.

The next step is adding 'hotel' schema to datasets in http://www.mockaroo.com/. This step described above.

The next schema is 'room'. There are such filds, its types and options:
-----------------------------------------------------------------------------------------------------
| Field Name 	         | Type 	     | Options 						    |
-----------------------------------------------------------------------------------------------------
| _id	     	         | MongoDB ObjectID  | none						    |
| hotel_id 	         | Dataset Column    | hotel, _id_$oid, random				    |
| type_of_room           | Custom List	     | Lux, Halflux, Standard, Economy; 		    |
|			 | 		     | Distribution Type: random			    |
| guest_amount           | Number	     | min: 1, max: 4					    |
| price		         | Number	     | min: 100, max: 10000				    |
| aditional_service[5-7] | Custom List	     | WiFi, Outdoor Pool, Non-smoking Rooms, Pet Friendly, |
|			 |		     | Family Rooms, Bar, TV, Air conditioning, Phone, 	    |
|			 |		     | Room Service, Facilities for Disabled Guests; 	    |
|			 |		     | Distribution Type: random			    |
-----------------------------------------------------------------------------------------------------

After that you can choose amount of rows and set JSON format. Then you need to click on the button 'Download Data'.
Further you must copy json-file to java project folder. Then you need to run following script:

public static void main(String[] args) throws IOException {
	BufferedReader br = new BufferedReader(new FileReader("room.json"));
	try {
		StringBuilder sb = new StringBuilder();
		String line = br.readLine();

		while (line != null) {
			sb.append(line);
			sb.append(System.lineSeparator());
			line = br.readLine();
		}
		String everything = sb.toString();
		String updated = everything.replace("{\"$oid\":", "ObjectId(");
		String updated2 = updated.replace("hotel_id\":", "hotel_id\":ObjectId(");
		String updated3 = updated2.replace("\",\"type_of_room", "\"),\"type_of_room");
		String updated4 = updated3.replace("aditional_servisces", "aditional_services");
		String updated5 = updated4.replace("\"},\"", "\"),\"");
		System.out.println("db.room.insertMany(" + updated5 + ")");
	} finally {
		br.close();
	}
}

After this action you need to copy text from eclipse console to js-file that you created.

The next step is adding 'hotel' schema to the datasets in http://www.mockaroo.com/. This step described above.

The next schema is 'review'. There are such filds, its types and options:
-----------------------------------------------------------------------------
| Field Name   | Type 	          | Options 				    |
-----------------------------------------------------------------------------
| _id	       | MongoDB ObjectID | none				    |
| hotel_id     | Dataset Column   | hotel, _id_$oid, random		    |
| user_id      | MongoDB ObjectID | none				    |
| text         | Catch Phrase     | min: 2, max: 5			    |
| mark	       | Number		  | min: 100, max: 10000		    |
| created_date | Date	   	  | 12/26/2016 to 06/26/2017 in mongoDB ISO |
| updated_date | Date	          | 06/26/2017 to 12/26/2017 in mongoDB ISO |
-----------------------------------------------------------------------------

After that you can choose amount of rows and set JSON format. Then you need to click on the button 'Download Data'.
Further you must copy json-file to java project folder. Then you need to run following script:

public static void main(String[] args) throws IOException {
	BufferedReader br = new BufferedReader(new FileReader("review.json"));
	try {
		StringBuilder sb = new StringBuilder();
		String line = br.readLine();

		while (line != null) {
			sb.append(line);
			sb.append(System.lineSeparator());
			line = br.readLine();
		}
		String everything = sb.toString();
		String updated = everything.replace("{\"$oid\":", "ObjectId(");
		String updated2 = updated.replace("hotel_id\":", "hotel_id\":ObjectId(");
		String updated3 = updated2.replace("\",\"user_id", "\"),\"user_id");
		String updated4 = updated3.replace("{\"$date\":", "new Date(");
		String updated5 = updated4.replace("}}", ")}");
		String updated6 = updated5.replace("\"},\"", "\"),\"");
		System.out.println("db.review.insertMany(" + updated6 + ")");
	} finally {
		br.close();
	}
}

After this action you need to copy text from eclipse console to js-file that you created.

The next schema is 'booking'. There are such filds, its types and options:
-----------------------------------------------------------------------------
| Field Name   | Type 	          | Options 				    |
-----------------------------------------------------------------------------
| _id	       | MongoDB ObjectID | none				    |
| hotel_id     | Dataset Column   | hotel, _id_$oid, random		    |
| room_id      | MongoDB ObjectID | room, _id_$oid, random		    |
| user_id      | MongoDB ObjectID | none				    |
| created_date | Date		  | 12/15/2017 to 12/22/2017 in mongoDB ISO |
| updated_date | Date	   	  | 12/23/2017 to 06/31/2017 in mongoDB ISO |
| total_price  | Number	          | min: 100, max: 25000		    |
-----------------------------------------------------------------------------

After that you can choose amount of rows and set JSON format. Then you need to click on the button 'Download Data'.
Further you must copy json-file to java project folder. Then you need to run following script:

public static void main(String[] args) throws IOException {
	BufferedReader br = new BufferedReader(new FileReader("booking.json"));
	try {
		StringBuilder sb = new StringBuilder();
		String line = br.readLine();

		while (line != null) {
			sb.append(line);
			sb.append(System.lineSeparator());
			line = br.readLine();
		}
		String everything = sb.toString();
		String updated = everything.replace("{\"$oid\":", "ObjectId(");
		String updated2 = updated.replace("hotel_id\":", "hotel_id\":ObjectId(");
		String updated3 = updated2.replace(",\"room_id\":", "),\"room_id\":ObjectId(");
		String updated4 = updated3.replace("\",\"user_id", "\"),\"user_id");
		String updated5 = updated4.replace("{\"$date\":", "new Date(");
		String updated6 = updated5.replace("}}", ")}");
		String updated7 = updated6.replace("},\"check_in", "),\"check_in");
		String updated8 = updated7.replace("\"},\"", "\"),\"");
		System.out.println("db.booking.insertMany(" + updated8 + ")");
	} finally {
		br.close();
	}
}

After this action you need to copy text from eclipse console to js-file that you created.

After that you need to start mongodb, mongoshell, enter the command 'load("<path_to_script/<file_name>.js>")', press 'Enter' and you will get a database named hotel_db with filled documents.
