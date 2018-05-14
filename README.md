# TicTacToe - MVVM

MVVM with [Data Binding on Android](https://developer.android.com/topic/libraries/data-binding/) has the benefits of easier testing and modularity, while also reducing the amount of glue code that we have to write to connect the view + model.

## Model

The model is the Data + State + Business logic of our Tic-Tac-Toe application.
It’s the brains of our application so to speak. It is not tied to the view or controller, and because of this, it is reusable in many contexts.

## View

The view binds to observable variables and actions exposed by the viewModel in a flexible way. More on that in minute.

## ViewModel

The ViewModel is responsible for wrapping the model and preparing observable data needed by the view.
It also provides hooks for the view to pass events to the model. The ViewModel is not tied to the view however.

View ([tictactoe.xml](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/res/layout/tictactoe.xml) [menu_tictactoe.xml](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/res/menu/menu_tictactoe.xml) [TicTacToeActivity](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/view/TicTacToeActivity.java))
|
|
|
Invoke Action , Bind to Data
|
|
+
ViewModel ([ViewModel <Interface>](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/viewmodel/ViewModel.java) [TicTacToeViewModel](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/viewmodel/TicTacToeViewModel.java))
|
|
|
Interact with
|
|
+
Model ([Board](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/model/Board.java) [Cell](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/model/Cell.java) [Player](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/model/Player.java))

Let’s take a closer look at the some of the moving parts here, starting with the ViewModel. [TicTacToeViewModel](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/viewmodel/TicTacToeViewModel.java)

A couple excerpts from the [view tictactoe.xml](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/res/layout/tictactoe.xml) to see how these variables and actions are bound.

## Evaluation

Unit testing is even easier now, because you really have no dependency on the view.
When testing, you only need to verify that the observable variables are set appropriately when the model changes.
There is no need to mock out the view for testing as there was with the MVP pattern.

## MVVM  Concerns

- *Maintenance* - Since views can bind to both variables and expressions, extraneous presentation logic can creep in over time, effectively adding code to our XML.
To avoid this, always get values directly from the ViewModel rather than attempt to compute or derive them in the views binding expression.
This way the computation can be unit tested appropriately.
