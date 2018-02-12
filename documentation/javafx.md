JavaFX – Application Structure
The class containing main() method extends application 
   import javafx.application.Application;
main method has launch(args); which calls start() method internally
start() is an abstract method and need to be implemented
primary stage is created as input for start method start(Stage primaryStage)
  @override 
  public void start(Stage primaryStage) throws Exception{} 

inside start
1. Scene Graph - prepare scene graph with required nodes 
     Scene graph is contained within Scene.
     Need to create root node which can be one of Group, Region or WebView class
	Group
	   import javafx.scene.Group;
	   Group root = new Group();
	   getChildren() method of Group class can be use to retrieve observable list
	   ObservableList list = root.getChildren();
	   Text object can be set as node
	   list.add(NodeObject);
	   Or when instantiating Group() class
	   Group root = new Group(NodeObject);
	Region
	   base of all node based UI controls like 
	   1.chart- - pie chart and XYChart and more subclasses for other charts
	   import javafx.scene.chart;
	   embed chart in application
	   2.pane – base for all pane – AnchorPane, BorderPane etc
	   import javafx.scene.layout
	   StackPane() pane = new StackPane();
	   ObservableList list = pane.newChildren();
	   list.add(NodeObject)
	   insert predefined layouts
	   3.Controls – base class for Accordion, ButtonBar etc
	   import javafx.scene.control
	   insert various UI elments in the application
	WebView – manages web engine and displays its content
	   






















2. Scene - prepare scene with required dimension and scene graph to it 
	Scene lives inside stage
	Scene represents GUI window with root (node and scene graph)
	root node, height and width of the window can be passed to create new scene
	Only root is mandatory during instantiation
	import javafx.scene.Scene;
	import javafx.scene.paint.Color;
	Scene scene = new Scene(root);
	Scene scene = new Scene(root, width, height, background color);
3. Stage - prepare stage and add scene to it and display content of stage
	Stage contains all java window in JavaFx
	Object of this class has to be passed as parameter to start()
	set the title of window, set the scene in the stage and show scene
	import javafx.stage.Stage;
	@override
	public void start(Stage primaryStage) throws Exception{}
	primaryStage.setTitle(“Title”);
	primaryStage.setScene();
	primaryStage.show()

JavaFX application life cycle
1. start() - entry point
2. stop() - logic to stop application
3. init() - cannot create stage or scene in this method

launch() - static method usually called main method
1. instance of application class is created
2. init() method is called
3. start() method is called
4. launcher waits for application to finish and calls stop()

Terminating JavaFx
1. close all windows
2. Platform.exit();
3. System.exit(init);

https://www.tutorialspoint.com/javafx/javafx_application.htm 
examples:
  Empty Window
  Drawing straight line
  Displaying Text

JavaFx Text

import javafx.scene.text;
Text text = new Text();
String x = “test string”;
text.setText(x);
text.setX(50);
text.setY(50);
Group root = new Group(text);
Scene scene = new Scene(root, 50,50)
primaryStage.setScene(scene);
primaryStage.show();

Four parameter
1.family
2.weight – FontWeight.BLACK, FontWeight.BOLD, EXTRA_BOLD, EXTRA_LIGHT, NORMAL, LIGHT, MEDIUM,
3.posture – FontPosture.ITALIC, FontPosture.REGULAR
4.size

text.setFont(Font.font(“verdana”,FontWeight.BOLD, FontPosture.REGULAR, 20);

Stroke and Color
import javafx.scene.shape;
Text color inside
text.setFill(Color.BEIGE);
text thickness
text.setStrokeWidth(2);
outside lining of text
text.setStroke(COLOR.BLUE);

Other Decoration
text1.strikeThrough(true);
text2.setUnderline(true);
Group root = new Group(text1, text2);

JavaFX Event Handling

an even occurs when user interacts with application
1. mouse click
2. keyboard
3. selecting an item from list
4. scrolling page

Types of Events
1.Foreground Events – require direct user interaction.
2.Background Events 
	operating system interruptions
	hardware or software failure
	timer expiry

Events in JavaFX
1.Mouse Event – mouse click (mouse clicked, mouse pressed,
	mouse released, mouse moved, mouse entered target,
	mouse exited target etc.)
2.Key Event – key stroke (key pressed, key released, key typed)
3.Drag Event – mouse drag (drag entered, drag dropped drag entered target)
4.Window Event – Windows showing/hiding (window hiding, window shown)

Event Handling
mechanism that controls the event and decides what should happen
if an even occurs.
Every event has 
1.Target – node on which an even occurred. Target can be window, scene and node.
2.Source – The source from which the event is generated. Eg mouse click
3.Type – Type of occurred event. Mouse pressed, mouse released






Circle circle = new Circle();
//Creating the mouse event handler 
 EventHandler<MouseEvent> eventHandler = new EventHandler<MouseEvent>() { 
    @Override 
    public void handle(MouseEvent e) { 
      System.out.println("Hello World"); 
      circle.setFill(Color.DARKSLATEBLUE);
    } 
 };  
 //Registering the event filter 
 circle.addEventFilter(MouseEvent.MOUSE_CLICKED, eventHandler); 
 circle.removeEventFilter(MouseEvent.MOUSE_CLICKED, eventHandler);

 //add and remove event handlers
 circle.addEventHandler(MouseEvent.MOUSE_CLIKCED, eventhandler); 
 circle.addEventHandler(MouseEvent.MOUSE_CLIKCED, eventhandler); 




BorderPane – can have menu, tool bar etc
