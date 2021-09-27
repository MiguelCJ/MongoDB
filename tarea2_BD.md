Miguel Ángel Cifuentes Jiménez
168274

- 4.
db.tweets.aggregate([
	{ $project: {_id:0, "user.lang": 1,  hrsSub: { $substr: ["$created_at", 11, 2] } } },
	{$match:{"user.lang":'es'}},
	{$sortByCount:"$hrsSub"}])


- 5.
db.tweets.aggregate([
	{$project: { "user.location": 1, minY:{$min:{yearSub: { $substr: ["$user.created_at", 26, -1] } } }}},
	{$match:{"minY.yearSub":'2006'}},
	{$sortByCount:"$user.location"}])

- 6.

# 7:00:00 a 18:59:59
db.tweets.aggregate([
	{ $project: {_id:0, "user.location": 1,  hrsSub: { $substr: ["$created_at", 11, 2] } } },
	{$match:{hrsSub:'18'}},
	{$sortByCount:"$user.location"}])

# 19:00:00 a 6:59:59
db.tweets.aggregate([
	{ $project: {_id:0, "user.location": 1,  hrsSub: { $substr: ["$created_at", 11, 2] } } },
	{$match:{$or:[{hrsSub:'20'},{hrsSub:'19'}]}},
	{$sortByCount:"$user.location"}])

