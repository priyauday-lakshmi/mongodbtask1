1) Find all the information about each products

db.getCollection('product').find({});

2) Find the product price which are between 400 to 800

db.getCollection('product').find({product_price: { $gt: 400, $lt: 800 }});

3) Find the product price which are not between 400 to 600

db.getCollection('product').find({product_price: {$not: { $gte: 400, $lte: 600 }}});

4) List the four product which are grater than 500 in price

db.getCollection('product').find({product_price:{$gt:500}}).limit(4)

5) Find the product name and product material of each products

db.getCollection('product').find({},{ product_name: 1, product_material: 1 });

6) Find the product with a row id of 10

db.getCollection('product').find({id: '10'});

7) Find only the product name and product material

db.getCollection('product').find({},{ product_name: 1, prodduct_material: 1 });

8) Find all products which contain the value of soft in product material

db.getCollection('product').find({product_material: 'Soft'});

9) Find products which contain product color indigo and product price 492.00

db.getCollection('product').find({$and: [{ product_price: 492 },{ product_color: 'indigo' }]});

10) Delete the products which product price value are same
db.getCollection("product").aggregate([
{
$group: {
_id: '$product_price',
count: { $sum: 1 }
}
},
{
$match: {
count: { $gt: 1 }
}
}
]).forEach((e) => {
db.getCollection("product").deleteMany({ product_price: e._id });
