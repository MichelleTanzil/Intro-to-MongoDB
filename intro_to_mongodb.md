<!-- Intro to MongoDB -->

<!-- Create a database called 'my_first_db'. -->
use my_first_db

<!-- Create students collection. -->
db.createCollection('students')

<!-- Each document you insert into this collection should have the following format: ({name: STRING, home_state: STRING, lucky_number: NUMBER, birthday: {month: NUMBER, day: NUMBER, year: NUMBER}}) -->
Create 5 students with the appropriate info.
db.students.insert({name: 'Michelle', home_state: 'SG', lucky_number: 3, birthday: {month: 07, day: 21, year: 1993}})
db.students.insert({name: 'Kevin', home_state: 'CA', lucky_number: 5, birthday: {month: 07, day: 22, year: 1994}})
db.students.insert({name: 'Mark', home_state: 'AZ', lucky_number: 6, birthday: {month: 07, day: 23, year: 1995}})
db.students.insert({name: 'Bailey', home_state: 'NV', lucky_number: 7, birthday: {month: 07, day: 24, year: 1996}})
db.students.insert({name: 'Shaun', home_state: 'IL', lucky_number: 8, birthday: {month: 06, day: 08, year: 1995}})

<!-- Get all students. -->
db.students.find().pretty()

<!-- Retrieve all students who are from California (San Jose Dojo) or Washington (Seattle Dojo). -->
db.students.find( { $or: [{home_state: 'CA'}, {home_state: 'WA'}]})

<!-- Get all students whose lucky number is: -->
<!-- greater than 3 -->
db.students.find({lucky_number: {$gt: 3}})

<!-- less than or equal to 10 -->
db.students.find({lucky_number: {$lte: 10}})

<!-- between 1 and 9 (inclusive) -->
db.students.find( { $and: [{lucky_number: {$gte: 1}}, {lucky_number: {$lte: 9}}]})

<!-- Add a field to each student collection called 'interests' that is an ARRAY. -->
<!-- It should contain the following entries: 'coding', 'brunch', 'MongoDB'. Do this in ONE operation. -->
db.students.updateMany({}, {$set:{interests: ['coding', 'brunch', 'MongoDB']}})

<!-- Add some unique interests for each particular student into each of their interest arrays. -->
db.students.update({name: 'Michelle'}, {$push:{interests: 'games'}})
db.students.update({name: 'Kevin'}, {$push:{interests: 'TV'}})
db.students.update({name: 'Mark'}, {$push:{interests: 'Food'}})
db.students.update({name: 'Bailey'}, {$push:{interests: 'Reading'}})
db.students.update({name: 'Shaun'}, {$push:{interests: 'Sleep'}})

<!-- Add the interest 'taxes' into someone's interest array. -->
db.students.update({name: 'Michelle'}, {$push:{interests: 'taxes'}})

<!-- Remove the 'taxes' interest you just added. -->
db.students.update({name: 'Michelle'}, {$pop:{interests: 1}})
db.students.update({name: 'Michelle'}, {$pull:{interests: 'taxes'}})

<!-- Remove all students who are from California. -->
db.students.remove({home_state: 'CA'})

<!-- Remove a student by name.  -->
db.students.remove({name: 'Mark'})

<!-- Remove a student whose lucky number is greater than 5 (JUST ONE) -->
db.students.remove({lucky_number: {$gt: 5}}, true)

<!-- Add a field to each student collection called 'number_of_belts' and set it to 0. -->
db.students.updateMany({}, {$set:{number_of_belts: 0}})

<!-- Increment this field by 1 for all students in Washington (Seattle Dojo). -->
db.students.updateMany({home_state: 'WA'}, {$inc: {number_of_belts: 1}})

<!-- Rename the 'number_of_belts' field to 'belts_earned' -->
db.students.updateMany({}, {$rename: {number_of_belts: 'belts_earned'}})

<!-- Remove the 'lucky_number' field. -->
db.students.updateMany({}, {$unset: {lucky_number: ''}})

<!-- Add a 'updated_on' field, and set the value as the current date. -->
db.students.updateMany({}, {$currentDate: {"updated_on": {$type: "date"}}})
