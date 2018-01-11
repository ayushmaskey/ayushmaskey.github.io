

#add package
meteor npm install --save simpl-schema				#package to provide constraint on sturcture of Mongo documents
meteor add aldeed:collection2-core				#monitors rules in simpl-schema and makes sure Mongo document does not violate it
metero add session						#store data for the given session
meteor add reactive-dict					#stores temporary reactive state of client, when it does not have to got to the server, update only my ui
meteor add accounts-ui accounts-password accounts-facebook	# add authentication

#remove package
meteor remove insecure						#unauthenticated clients cannot write to database
meteor remove autopublish					#only things specified by publish and subsribe will show in client




meteor mongo							#view server side mongo



meteror deploy chatApp111					#deploy to meteor server - free and paid versions 
meteor bundle							#use in server with nodejs
meteor list-platforms						#list all the platform currently compatible with
meteor add-platform ios						#add package necessary for IOS
meteor run ios


meteor update							#update packages
