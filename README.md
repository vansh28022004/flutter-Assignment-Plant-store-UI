# flutter-Assignment-Plant-store-UI

import 'package:flutter/material.dart';

void main() => runApp(PlantStoreApp());

class PlantStoreApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Plant Store UI',
      debugShowCheckedModeBanner: false,
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  final List<Map<String, String>> plants = [
    {"name": "Peace Lily", "price": "\$20", "image": "assets/plant1.png"},
    {"name": "ZanZiber Gem", "price": "\$25", "image": "assets/plant2.png"},
    {"name": "Pothos", "price": "\$36", "image": "assets/plant3.png"},
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Color(0xFFD8EAD9),
      body: SafeArea(
        child: Padding(
          padding: const EdgeInsets.all(16.0),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Text("🌱 Hello Mia",
                  style: TextStyle(fontSize: 22, fontWeight: FontWeight.bold)),
              Text("Take care of your plants!",
                  style: TextStyle(color: Colors.grey[700])),
              SizedBox(height: 16),
              TextField(
                decoration: InputDecoration(
                  hintText: "Search",
                  prefixIcon: Icon(Icons.search),
                  filled: true,
                  fillColor: Colors.white,
                  border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(12),
                      borderSide: BorderSide.none),
                ),
              ),
              SizedBox(height: 16),
              Text("Recently Viewed",
                  style: TextStyle(fontWeight: FontWeight.bold)),
              SizedBox(height: 10),
              Row(
                children: [
                  buildPlantCard(
                      "Orchid Cactus", "Indoor Plant", "assets/plant1.png"),
                  SizedBox(width: 10),
                  buildPlantCard("Hoya", "Indoor Plant", "assets/plant2.png"),
                ],
              ),
              SizedBox(height: 20),
              Row(
                children: ["Popular", "Outdoor", "Indoor", "Top Pick"].map((e) {
                  return Padding(
                    padding: const EdgeInsets.only(right: 16.0),
                    child: Text(
                      e,
                      style: TextStyle(
                          fontWeight: e == "Popular"
                              ? FontWeight.bold
                              : FontWeight.normal,
                          color: e == "Popular" ? Colors.green : Colors.black),
                    ),
                  );
                }).toList(),
              ),
              SizedBox(height: 10),
              Container(
                height: 120,
                child: ListView.builder(
                  scrollDirection: Axis.horizontal,
                  itemCount: plants.length,
                  itemBuilder: (context, index) {
                    final plant = plants[index];
                    return GestureDetector(
                      onTap: () => Navigator.push(context,
                          MaterialPageRoute(builder: (_) => DetailScreen())),
                      child: Container(
                        width: 100,
                        margin: EdgeInsets.only(right: 16),
                        child: Column(
                          children: [
                            Image.asset(plant["image"]!, height: 70),
                            Text(plant["name"]!,
                                style: TextStyle(fontWeight: FontWeight.bold)),
                            Text(plant["price"]!,
                                style: TextStyle(color: Colors.green)),
                          ],
                        ),
                      ),
                    );
                  },
                ),
              ),
              Spacer(),
              Container(
                padding: EdgeInsets.all(16),
                decoration: BoxDecoration(
                  color: Colors.orange[100],
                  borderRadius: BorderRadius.circular(20),
                ),
                child: Row(
                  children: [
                    Icon(Icons.local_shipping, color: Colors.green),
                    SizedBox(width: 10),
                    Text("Free Shipping Above \$50",
                        style: TextStyle(fontWeight: FontWeight.bold)),
                    Spacer(),
                    Icon(Icons.delivery_dining),
                  ],
                ),
              )
            ],
          ),
        ),
      ),
    );
  }

  Widget buildPlantCard(String name, String category, String imagePath) {
    return Container(
      width: 120,
      padding: EdgeInsets.all(10),
      decoration: BoxDecoration(
          color: Colors.white, borderRadius: BorderRadius.circular(12)),
      child: Column(
        children: [
          Image.asset(imagePath, height: 50),
          Text(name, style: TextStyle(fontWeight: FontWeight.bold)),
          Text(category, style: TextStyle(color: Colors.grey)),
        ],
      ),
    );
  }
}

class DetailScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Color(0xFFD8EAD9),
      body: SafeArea(
        child: Column(
          children: [
            Container(
              padding: EdgeInsets.all(16),
              height: 350,
              child: Column(
                children: [
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      BackButton(),
                      Icon(Icons.favorite_border),
                    ],
                  ),
                  SizedBox(height: 10),
                  Image.asset("assets/plant1.png", height: 150),
                  SizedBox(height: 10),
                  Text("Peace Lily",
                      style:
                          TextStyle(fontSize: 24, fontWeight: FontWeight.bold)),
                  SizedBox(height: 10),
                  Text("Type: Small",
                      style: TextStyle(color: Colors.grey[700])),
                  Text("Category: Indoor Plant"),
                  Text("Price: \$40.00",
                      style: TextStyle(fontWeight: FontWeight.bold)),
                ],
              ),
            ),
            Padding(
              padding: const EdgeInsets.symmetric(horizontal: 24.0),
              child: Row(
                mainAxisAlignment: MainAxisAlignment.spaceBetween,
                children: [
                  infoBox(Icons.light_mode, "Light", "37%"),
                  infoBox(Icons.water_drop, "Water", "2"),
                  infoBox(Icons.thermostat, "Temp", "25°C"),
                ],
              ),
            ),
            SizedBox(height: 20),
            Padding(
              padding: const EdgeInsets.all(16.0),
              child: Container(
                padding: EdgeInsets.all(16),
                decoration: BoxDecoration(
                    color: Colors.white,
                    borderRadius: BorderRadius.circular(16)),
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text("About Peace Lily",
                        style: TextStyle(fontWeight: FontWeight.bold)),
                    SizedBox(height: 8),
                    Text(
                        "The peace lily plant is well known for its air-purifying abilities as a houseplant. It’s great at breaking down and neutralizing toxic gases like carbon..."),
                    TextButton(onPressed: () {}, child: Text("Read More")),
                  ],
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }

  Widget infoBox(IconData icon, String label, String value) {
    return Column(
      children: [
        Icon(icon, color: Colors.green),
        Text(label),
        Text(value, style: TextStyle(fontWeight: FontWeight.bold)),
      ],
    );
  }
}
