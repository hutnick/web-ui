import 'package:flutter/material.dart';
import 'package:english_words/english_words.dart';


void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {

  // This widget is the root of your application.

  @override
  Widget build(BuildContext context) {
    return MaterialApp(

      title: 'Name_Gen',

      home: RandomWords(),

    );
  }
}


// Stateful Widget musi zawierac przynajmniej 2 klasy
// 1 - '_StatefulWidget' - immutable instance
// 2 - '_State' - states changes

// 'RandomWords' extnds StatefulWidget
// '@override' >>> _classState1 createState() => WidgetState1();


class RandomWords extends StatefulWidget {
  @override
  RandomWordsState createState() => RandomWordsState();
}

// WidgetState1 extnds State<Widget>
// @override build() method + context

class RandomWordsState extends State<RandomWords> {

// Actual 'class'

  final _suggestions = <WordPair>[];
  final _biggerFont = const TextStyle(fontSize: 18.0);

  @override 
  Widget build(BuildContext context) {
    return Scaffold(

      appBar: AppBar(

        title: Text('Name_Gen'),
      backgroundColor: Colors.orange),

      body: _buildSuggestions(), // Widget1

    );
  }

// Widget1

  Widget _buildSuggestions(){
    return ListView.builder(

      padding: const EdgeInsets.all(14),
      itemBuilder: (context, i) {

        if (i.isOdd) return Divider();

        final index = i ~/ 2;
        if (index >= _suggestions.length) {         
          _suggestions.addAll(generateWordPairs().take(10));
        }
        return _buildRow(_suggestions[index]); // Widget2
      },
    );

  }

// Widget2 

Widget _buildRow(WordPair pair) {
  return ListTile(
    title: Text(
      pair.asPascalCase,
      style: _biggerFont,  
    ),
  );
}

}

