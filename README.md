import 'package:flutter/material.dart';

void main() => runApp(CalculatorApp());

class CalculatorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CalculatorScreen(),
    );
  }
}

class CalculatorScreen extends StatefulWidget {
  @override
  _CalculatorScreenState createState() => _CalculatorScreenState();
}

class _CalculatorScreenState extends State<CalculatorScreen> {
  String output = "0";
  String input = "";
  double num1 = 0.0;
  double num2 = 0.0;
  String operand = "";

  void _buttonPressed(String buttonText) {
    if (buttonText == "C") {
      setState(() {
        output = "0";
        input = "";
        num1 = 0.0;
        num2 = 0.0;
        operand = "";
      });
    } else if (buttonText == "+" || buttonText == "-" || buttonText == "x" || buttonText == "/") {
      setState(() {
        num1 = double.parse(output);
        operand = buttonText;
        input += buttonText;
        output = "0";
      });
    } else if (buttonText == "=") {
      setState(() {
        num2 = double.parse(output);
        if (operand == "+") {
          output = (num1 + num2).toString();
        }
        if (operand == "-") {
          output = (num1 - num2).toString();
        }
        if (operand == "x") {
          output = (num1 * num2).toString();
        }
        if (operand == "/") {
          if (num2 != 0) {
            output = (num1 / num2).toString();
          } else {
            output = "Error";
          }
        }
        input = "";
        operand = "";
      });
    } else {
      setState(() {
        if (output == "0") {
          output = buttonText;
        } else {
          output += buttonText;
        }
        input += buttonText;
      });
    }
  }

  Widget buildButton(String buttonText) {
    return Expanded(
      child: TextButton(
        onPressed: () => _buttonPressed(buttonText),
        child: Text(
          buttonText,
          style: TextStyle(fontSize: 50.0,color: Colors.black,
            ),
        ),

      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Calculator'),
      ),
      body: Container(color: Colors.white,
        child: Column(
          children: <Widget>[
            Container(
              alignment: Alignment.centerRight,
              padding: EdgeInsets.symmetric(horizontal: 12.0, vertical: 24.0),
              child: Text(
                input,
                style: TextStyle(fontSize: 30.0,color: Colors.black),
              ),
            ),
            Container(
              alignment: Alignment.centerRight,
              padding: EdgeInsets.symmetric(horizontal: 12.0, vertical: 24.0),
              child: Text(
                output,
                style: TextStyle(fontSize: 60.0, fontWeight: FontWeight.bold),
              ),
            ),
            /*Expanded(
              child: Divider(),
            )*/
            const SizedBox(height: 150,),
            Container(
              child: Center(
                child: Column(
                  children: <Widget>[
                    Row(
                      children: <Widget>[
                        buildButton("7"),
                        buildButton("8"),
                        buildButton("9"),
                        buildButton("/"),
                      ],
                    ),
                    Row(
                      children: <Widget>[
                        buildButton("4"),
                        buildButton("5"),
                        buildButton("6"),
                        buildButton("x"),
                      ],
                    ),
                    Row(
                      children: <Widget>[
                        buildButton("1"),
                        buildButton("2"),
                        buildButton("3"),
                        buildButton("-"),
                      ],
                    ),
                    Row(
                      children: <Widget>[
                        buildButton("C"),
                        buildButton("0"),
                        buildButton("="),
                        buildButton("+"),
                      ],
                    ),
                  ],
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
          
