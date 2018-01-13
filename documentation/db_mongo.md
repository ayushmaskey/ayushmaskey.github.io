meteor mongo						#start mongo shell
show dbs						#show all databases
show collections					#show all collections

#create
db.createCollection("collectionName");			#create new collection
#or from Meteor
PlayerList = new Mongo.Collection('players')

#insert
db.people.insert({first:"ayush",last:"maskey",...});	#insert a document to collection
#or
PlayerList.insert();

#filter
db.people.find();					#get all documents from collection in mongo console
db.people.find({ city: "Kailua" });			#filter by city
db.people.find({ age: { $lt:35 } })			#filter by age less than 35
#or
PlayerList.find();					#not quite readable in console
PlayerList.find().fetch();				#readable format in chrome console
PlayerList.find( {name:'Ayush'}).fetch()		#filter in browser console
PlayerList.find().count();				#num of documents in collection

#update
db.people( {first:"Ayush", last:"Maskey"}, { $set: {age:60} } );


#delete
db.people.deleteOne( {first:"Ayush", last: "Maskey" } );

#order by
db.people.find().sort( {age:1} );
db.people.find().sort( {age:-1} );
