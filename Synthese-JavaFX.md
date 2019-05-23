```java
package application;

import java.util.Optional;

import javafx.beans.value.ChangeListener;
import javafx.beans.value.ObservableValue;
import javafx.collections.ObservableList;
import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.ListView;
import javafx.scene.control.SelectionMode;
import javafx.scene.control.TextInputDialog;

public class FenetreController implements ChangeListener<String>{
	@FXML
	private Button _delButton;
	
	@FXML
	private ListView<String> _list;
	
	@FXML
	private Label _bResultat;
	
	public void clearList(ActionEvent event) {
		_list.getItems().clear();
	}
	
	@FXML
	private void initialize() {
		_list.getSelectionModel().setSelectionMode(SelectionMode.MULTIPLE);
		
		_delButton.setDisable(true);
		
		_list.getSelectionModel().selectedItemProperty().addListener(this);;
	}
	
	
	public void delList(ActionEvent event) {
		ObservableList<Integer> selectedIndices =
		_list.getSelectionModel().getSelectedIndices();
		for (int i= selectedIndices.size()-1;i>=0;i--) {
		int indice = selectedIndices.get(i).intValue();
		_list.getItems().remove(indice);
		}
	}
	
	public void addList(ActionEvent event) {
		TextInputDialog inDialog = new TextInputDialog("");
		inDialog.setTitle("Saisissez un texte");
		inDialog.setHeaderText(null);
		inDialog.setContentText("Votre texte :");
		Optional<String> textIn = inDialog.showAndWait();
		if (textIn.isPresent() && !textIn.get().isEmpty()) {
		_list.getItems().add(textIn.get());
		}
	}
		
		
	public void changed(ObservableValue<? extends String> observable, String oldValue, String newValue ) {
		_delButton.setDisable(_list.getSelectionModel().getSelectedItems().size()==0);
	}
	
	
}
```

按下按钮在console里显示相关信息,fxml要做个链接

```java
public void AfficherPath(ActionEvent event) {
        System.out.println(getPath());
}
```

---



### Framework

```java
package application;
	
import javafx.application.Application;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.layout.BorderPane;


public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {
			GridPane root = new GridPane();	//Lier le fxml ici: à remplacer
			Scene scene = new Scene(root,450,450,Color.BLACK);	//Parametrer la taille et couleur
			scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());
			primaryStage.setScene(scene);
      primaryStage.setTitle("This is my title");	//Titre
			primaryStage.show();
		} catch(Exception e) {
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) {
		launch(args);
	}
}

```



### Lier le fichier FXML

```java
GridPane root = FXMLLoader.load(getClass().getResource("view.fxml")); //À remplacer 
```



### Forme

#### 1. Rectangle

   ```java
//1er
Rectangle r = new Rectangle(100, 100, 80, 120);	//Coordonée, width(长), height
r.setFill(Color.BLACK);	//Remplir la couleur

//2ième
Rectangle ra = new Rectangle(100, 50, Color.ORANGE);
ra.setX(10);
ra.setY(20);
ra.setArcWidth(30);
ra.setArcHeight(20);
   ```

#### 2. Cylinder

   ```java
   Cylinder c = new Cylinder(25, 100);	//Créer un cylindre
   c.setTranslateX(50);	//Déplacer 50 vers axe X
   c.setTranslateY(100);	//Déplacer 100 vers axe Y
   c.setRotationAxis(new Point3D(10, 10, 10));	//Devenir 3D: x, y, z
   c.setRotate(45);	// Tourner 50 
   ```

#### 3. Circle

   ```java
   Circle ce = new Circle(280, 100, 25);	//Créer un cycle
   ce.setFill(Color.CHARTREUSE);	//Remplir le couleur
   ```

**4.** **Ajouter dans la groupe `root`**

   ```java
root.getChildren().addAll(r,c,ce);
   ```

#### 5. Line

```java
Line l = new Line(20, 140, 80, 180);	//x, y, width, height
l.setStroke(Color.CRIMSON);	//Couleur
l.setStrokeWidth(4);	//En gras
```

#### 6. Polyline (折线)

```java
Polyline pL = new Polyline(new double[] {//Début, point1, point2, fin
                    150.0, 50.0, 200.0, 20.0,	
                    220.0, 50.0,
                    250.0, 20.0
            });
pL.setStroke(Color.DARKRED);	//Couleur
pL.setStrokeWidth(3);	//En gras
```

#### 7. Polygon(多边形)

```java
Polygon p = new Polygon();
            p.getPoints().addAll(new Double[] {10.0, 280.0, 20.0, 220.0, 50.0, 240.0, 5.0, 180.0});	//x1,y1 x2,y2 x3,y3
p.setStroke(Color.DARKORCHID);	//Couleur de fil
p.setStrokeWidth(3);	//En gras
p.setFill(Color.LIGHTSALMON);	//Couleur contenu
```

#### 8. Ellipse(椭圆形)

```java
Ellipse e = new Ellipse (200, 150, 40, 20);	//(double centerX, double centerY, double radiusX, double radiusY)
e.setFill(Color.CORNFLOWERBLUE);
```

#### 9. Arc(弧)

```java
Arc a = new Arc(175.0, 240.0, 40.0, 40.0, 0.0, 90.0);	//(double centerX, double centerY, double radiusX, double radiusY, double startAngle, double length)
a.setStroke(Color.BLUEVIOLET);
a.setStrokeWidth(3);
a.setFill(null);
```

#### 10. QuadCurve (曲线)

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTt-qM7ycILuOm7tVgt3DG1Z27Y_vPXSWqZHjW_MAF9ovCI0kld1g)

```java
QuadCurve qc = new QuadCurve(50, 280, 100, 145, 150, 270);	//start, control, end
qc.setStroke(Color.RED);
qc.setFill(null);
```

11. CubicCurve

    ![](https://www.tutorialspoint.com/javafx/images/bezier_curves.jpg)

```java
CubicCurve cC = new CubicCurve(150, 280, 185, 200, 195, 300, 250, 230);
cC.setStroke(Color.BLUE);
cC.setFill(null);
```

> `root.getChildren().addAll(l, pL,p, ra, rb, c, cC); `

### Containers

#### 1. HBox et VBox

```java
HBox root = new HBox();
VBox root = new VBox();


root.setPadding(new Insets(10));	//Paramétrer l'intervalle pendant ces contenus dans H(V)Box

root.setMargin(b1, new Insets(10));	//Paramétrer l'intervalle sur le bouton b1
```

#### 2. GridPane

```java
GridPane g = new GridPane();//Créer
...
g.setPadding(new Insets(10));	//Intervalle autour

GridPane.setMargin(b1, new Insets(10));	//Paramétrer Button b1(autour) dedans la GridPane

g.add(b1, 1, 0);	//Ajouter boutons dans (1,0)[à partir de 0]
```

#### 3. Pane

```java
Pane root = new Pane();
```



### Controls

#### 1. ListView(Affichage)

```java
ListView<String> listview = new ListView<String>();	//Créer un listview
l.setMaxHeight(200);	//Paramétrer la hauteur
root.setPadding(new Insets(10));	//Autour de liste
```

   

#### 2. Button

```java
Button b1 = new Button("Add..");
b1.setMinWidth(100);	//Width minimal
b1.setMinHeight(20);	//Haute minial
```

##### 2.1 Fonctions

###### 2.1.1 DelButtonController

```java
package application;

import javafx.collections.ObservableList;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.scene.control.ListView;

public class DelButtonController implements EventHandler<ActionEvent> {	//Ajouter une action extends EventHandler
    ListView<String> _list;	

    public DelButtonController(ListView<String> list){	//Constructeur
        this._list = list;
    }

    public void handle (ActionEvent event){
        ObservableList<Integer> selecteIndices = _list.getSelectionModel().getSelectedIndices();

        for (int i = selecteIndices.size()-1;i>=0;i--){	//Supprimer jusqu'à la fin
            int indice = selecteIndices.get(i).intValue();
            _list.getItems().remove(indice);
        }
    }
}
```

###### 2.1.2 Disable

```java
//l:  ListView<String>
l.getSelectionModel().selectedIndexProperty().addListener(
                    (observable,oldValue,newValue)->{
                        b3.setDisable(
                                l.getSelectionModel().getSelectedItems().size()==0);
                    }

            );	
```

###### 2.1.3 Afficher un alert quand on clique le bouton

> **Dans Containers**

```java
root.addEventFilter(ActionEvent.ACTION, new EventHandler<ActionEvent>(){	//On ajoute la fonction sur **HBOX**
                public void handle(ActionEvent e){	//Constructeur
                    Alert dialog=new Alert(AlertType.INFORMATION);	//Implémenter un alert dialog
                    dialog.setTitle("Filtre");	//Titre de dialog
                    dialog.setHeaderText("**Un filtre a été déclenché**");	//Afficher le contenu
                    dialog.setContentText("Evénement"+e.getEventType()+"\n Cible:"+e.getTarget().getClass().getName());
                    dialog.showAndWait();	//Afficher cette dialogue
                    //e.consume(); supprimer cet instruction on continuer ver fcts suit
                }
            });
```

![Dialog](http://t.cn/EomVT2a)

> À utiliser

```java
DelButtonController delBC=new DelButtonController(l);	//l: listview<String> à afficher la texte
b1.addEventHandler(ActionEvent.ACTION,delBC);	//On l'ajoute dans le boutou b1, ActionEvent.ACTION: On clique
```



###### 2.1.4 Ajouter la texte quand on clique le bouton

```java
b_Add.addEventHandler(ActionEvent.ACTION,new EventHandler<ActionEvent>(){	//Sur bouton
                        public void handle(ActionEvent event){	//On créer un handle
                            TextInputDialog inDialog=new TextInputDialog("Input Défaut");	//Créer un TextInput Dialog et paramétrer le contenu défaut
                            inDialog.setTitle("Saiair un text");	//Titre
                            inDialog.setHeaderText(null);
                            inDialog.setContentText("Votre texte:");	//Contenus
                            Optional<String>textIn=inDialog.showAndWait();
                            if(textIn.isPresent()&&!textIn.get().isEmpty()){
                                l.getItems().add(textIn.get());
                            }
                        }
                    }
            );
```

![](http://t.cn/EomIemJ)



###### 2.1.5 Supprimer tous dans la listview

```java
b3.setOnAction(new EventHandler<ActionEvent>(){
                public void handle(ActionEvent event){
                    l.getItems().clear();
                }
            });	//Ajouter une action sur le bouton
```



> !!! N'oublie pas de `root.getChildren().addAll(b1, b2, b3);` à la fin





##### 2.2 Code complet pour implémenter la fonction de bouton

[ZIP_Bouton_Fonction_Telecharger(Eclipse)](http://t.cn/EomMrn8)



##### 2.3 Bouton dans Controller avec FXML

1. Ensemble([ZIP](http://t.cn/EomoMyL))
2. 

![](http://t.cn/EomooCW)

```java
//Code complet pour afficher comme ci-dessus
//Controler.java
package application;

import java.util.Optional;

import javafx.beans.value.ChangeListener;
import javafx.beans.value.ObservableValue;
import javafx.collections.ObservableList;
import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.ListView;
import javafx.scene.control.SelectionMode;
import javafx.scene.control.TextInputDialog;

public class Controler implements ChangeListener<String>{
	@FXML
	private Button _delButton;
	
	@FXML
	private ListView<String> _list;
	
	@FXML
	private Label _bResultat;
	
	public void clearList(ActionEvent event) {
		_list.getItems().clear();
	}
	
	@FXML
	private void initialize() {
		_list.getSelectionModel().setSelectionMode(SelectionMode.MULTIPLE);
		
		_delButton.setDisable(true);
		
		_list.getSelectionModel().selectedItemProperty().addListener(this);;
	}
	
	
	public void delList(ActionEvent event) {
		ObservableList<Integer> selectedIndices =
		_list.getSelectionModel().getSelectedIndices();
		for (int i= selectedIndices.size()-1;i>=0;i--) {
		int indice = selectedIndices.get(i).intValue();
		_list.getItems().remove(indice);
		}
	}
	
	public void addList(ActionEvent event) {
		TextInputDialog inDialog = new TextInputDialog("");
		inDialog.setTitle("Saisissez un texte");
		inDialog.setHeaderText(null);
		inDialog.setContentText("Votre texte :");
		Optional<String> textIn = inDialog.showAndWait();
		if (textIn.isPresent() && !textIn.get().isEmpty()) {
		_list.getItems().add(textIn.get());
		}
	}
		
		
	public void changed(ObservableValue<? extends String> observable, String oldValue, String newValue ) {
		_delButton.setDisable(_list.getSelectionModel().getSelectedItems().size()==0);
	}
	
	
}
```

```html
//.FXML
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.geometry.Insets?>
<?import javafx.scene.control.Button?>
<?import javafx.scene.control.ListView?>
<?import javafx.scene.layout.HBox?>
<?import javafx.scene.layout.VBox?>

<HBox maxHeight="-Infinity" maxWidth="-Infinity" minHeight="-Infinity" minWidth="-Infinity" prefHeight="400.0" prefWidth="600.0" xmlns="http://javafx.com/javafx/11.0.1" xmlns:fx="http://javafx.com/fxml/1" fx:controller="application.Controler">
   <children>
      <ListView fx:id="_list" minHeight="250.0" minWidth="250.0">
         <HBox.margin>
            <Insets bottom="10.0" left="10.0" top="10.0" />
         </HBox.margin></ListView>
      <VBox prefHeight="200.0" prefWidth="100.0">
         <children>
            <Button minWidth="100.0" mnemonicParsing="false" onAction="#addList" text="add">
               <VBox.margin>
                  <Insets left="10.0" top="10.0" />
               </VBox.margin></Button>
            <Button fx:id="_delButton" minWidth="100.0" mnemonicParsing="false" onAction="#delList" text="delete">
               <VBox.margin>
                  <Insets left="10.0" top="10.0" />
               </VBox.margin></Button>
            <Button minWidth="100.0" mnemonicParsing="false" onAction="#clearList" text="clear">
               <VBox.margin>
                  <Insets left="10.0" top="10.0" />
               </VBox.margin></Button>
         </children>
      </VBox>
   </children>
</HBox>

```

```java
//Main.java
package application;
	
import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.layout.HBox;


public class Main extends Application {
	@Override
	//Je dépose sur Intellij
	public void start(Stage primaryStage) {
		try {
			HBox root = FXMLLoader.load(getClass().getResource("ex.fxml"));
			Scene scene = new Scene(root, 400, 250);
			scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());
			primaryStage.setScene(scene);
			primaryStage.show();
		} catch(Exception e) {
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) {
		launch(args);
	}
}

```



#### 3. Ajouter dans `root`

   ```java
root.getChildren().addAll(l, n1);	
   ```



#### 4. FXML

##### 4.1 Framework

```java
package application;
import javafx.fxml.FXML;
...

public class Controler implements ChangeListener<String>{
	@FXML	//Lier à FXML
	private Button _delButton;	//Définir un bouton
	......
	
	@FXML	//Private méthode avec @FXML
	private void initialize() {	
_list.getSelectionModel().setSelectionMode(SelectionMode.MULTIPLE);		
_delButton.setDisable(true);
_list.getSelectionModel().selectedItemProperty().addListener(this);;
	}

}
```

> Ensuite, on le lie dans SceneBuilder

##### 4.2 Lien dans SceneBuilder

> Dans main.java:
>
> `HBox root = FXMLLoader.load(getClass().getResource("ex.fxml"));`

1.

![](http://t.cn/EomajhA)

2.

![](http://t.cn/Eomanyk)

## Autre à commencer(按照老师课件顺序)

## 一 元素介绍

### 1.  Groupe


   ![](https://files.catbox.moe/ucdwcs.png)

```java
package application;
	
import javafx.application.Application;
import javafx.geometry.Point3D;
import javafx.stage.Stage;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.paint.Color;
import javafx.scene.shape.Circle;
import javafx.scene.shape.Cylinder;
import javafx.scene.shape.Rectangle;


public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {
			Group root = new Group();
			Scene scene = new Scene(root, 300, 300, Color.BLACK);
			
			
			Rectangle r = new Rectangle(100,100,80,120);
			r.setFill(Color.BLUE);
			Cylinder c = new Cylinder(25, 100);
			c.setTranslateX(50);
			c.setTranslateY(100);
			c.setRotationAxis(new Point3D(10, 10, 10));
			c.setRotate(45);
			Circle ce = new Circle(280, 100, 25);
			ce.setFill(Color.CHARTREUSE);
		    root.getChildren().addAll(r, c, ce);
		    
		    
			primaryStage.setScene(scene);
			primaryStage.show();
		} catch(Exception e) {
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) {
		launch(args);
	}
}

```

### 2. BorderPane

![](https://files.catbox.moe/0m8ely.png)

```java
package application;

import javafx.application.Application;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.BorderPane;
import javafx.scene.paint.Color;


public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {
			BorderPane root = new BorderPane();
			Scene scene = new Scene(root, 300, 300, Color.BLACK);

			Button top = new Button("Top");
			Button bottom = new Button("Bottom");
			Button left = new Button("Left");
			Button right = new Button("Right");
			Button center = new Button("Center");
			root.setTop(top);
			root.setBottom(bottom);
			root.setLeft(left);
			root.setRight(right);
			root.setCenter(center);

			primaryStage.setScene(scene);
			primaryStage.show();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

	public static void main(String[] args) {
		launch(args);
	}
}

```

### 2.2 BorderPane - ajout

![ ](https://files.catbox.moe/s2nu2g.png)

```java
package application;

import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.BorderPane;
import javafx.scene.paint.Color;


public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {
			BorderPane root = new BorderPane();
			Scene scene = new Scene(root, 300, 300, Color.BLACK);

			Button top = new Button("Top");
			Button bottom = new Button("Bottom");
			Button left = new Button("Left");
			Button right = new Button("Right");
			Button center = new Button("Center");
      
			BorderPane.setAlignment(top, Pos.CENTER);	//ajout
			BorderPane.setAlignment(right,Pos.BOTTOM_CENTER);	//ajout
			BorderPane.setMargin(bottom, new Insets(10));	//Tous les nodes sont 10 autour
			
			root.setTop(top);
			root.setBottom(bottom);
			root.setLeft(left);
			root.setRight(right);
			root.setCenter(center);

			primaryStage.setScene(scene);
			primaryStage.show();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

	public static void main(String[] args) {
		launch(args);
	}
}

```

### 3. HBOX

![](https://files.catbox.moe/l1zcpx.png)

```java
package application;

import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.BorderPane;
import javafx.scene.layout.HBox;
import javafx.scene.paint.Color;


public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {
			HBox root = new HBox();
			Scene scene = new Scene(root, 300, 300, Color.BLACK);

			
			Button n1 = new Button("Bouton 1");
			Button n2 = new Button("Bouton 2");
			//Bordures minimales de la boîte
			root.setPadding(new Insets(25, 30, 35, 40));	//Définit les espaces pour chaque bord : top, right, bottom puis left 1 seule valeurs données ð même marge pour tous les bords
			//espacement entre les noeuds
			root.setSpacing(20);	//Espacement horizontal eh entre chaque noeud
			root.getChildren().addAll(n1, n2);	//Alignement vertical/horizontal des noeuds

			primaryStage.setScene(scene);
			primaryStage.show();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

	public static void main(String[] args) {
		launch(args);
	}
}

```

#### 3.1 Supplémentaire

```java
static void setHgrow(Node c, Priority p)
```

Agrandir le composant c selon une priorité donnée p

​	• Priority.ALWAYS : toujours essayer d’agrandir à sa taille max

– En partageant l’espace dispo avec les autres composants ALWAYS

​	• Priority.NEVER : ne jamais essayer d’agrandir

​	• Priority.SOMETIMES : s’agrandir si possible

– Pas de composants avec priorité ALWAYS prenant tout l’espace

– En partageant l’espace dispo avec autres composants SOMETIMES



```java
static void setMargin(Node c, Insets m)
```

Fixer une marge m autour du composant c



### 4. VBox

Introduction :

– De haut en bas

– Comportement symétrique de HBox **(与Hbox一样)**



## 5. 整合1到4-Projet

But:

![](https://files.catbox.moe/nn9z2e.png)

### Partie 1 - StackPane

– Le premier au fond, le dernier au-dessus

– Ajout des noeuds dans StackPane s (comme HBox)

​	• `s.getChildren().add(node)`

​	• `s.getChildren().addAll(node1, node2, node3, …)`

– Utilisation

​	• mettre du texte sur une forme

​	• Superposer des formes pour avoir une forme complexe

– Alignement des noeuds dans le conteneur

​	• Méthode SetAlignment de la classe StackPane

​	– **Pour tous les noeuds** 

​		`void setAlignment(Pos p)`

​	– **Pour un noeud** 

​		`static void setAlignment (Node n, Pos p)`

Présentation 1

![](https://files.catbox.moe/lnlkge.jpg)

```java
package application;

import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.layout.StackPane;
import javafx.scene.paint.Color;
import javafx.scene.shape.Rectangle;
import javafx.scene.text.Font;
import javafx.scene.text.FontWeight;
import javafx.scene.text.Text;


public class Main extends Application {
	@Override
	public void start(Stage primaryStage) {
		try {
			StackPane root = new StackPane();	
			Scene scene = new Scene(root,400,400);
		
      //JPG
			Rectangle helpIcon = new Rectangle(40,40);
			helpIcon.setFill(Color.CORNFLOWERBLUE);
			
      //Texte help
      Text helpText = new Text("?");
			helpText.setFont(Font.font("Verdana", FontWeight.BOLD, 36));
			helpText.setFill(Color.WHITE);
			helpText.setStroke(Color.BLACK);
      
      //Ajouter
			root.getChildren().addAll(helpIcon, helpText);	//自动叠放
			
      //Mettre tous les noeuds centrés verticalement et alignés à droite
			root.setAlignment(Pos.CENTER_RIGHT);
			StackPane.setMargin(helpText, new Insets(0, 10, 0, 0));	//Autour

			primaryStage.setScene(scene);
			primaryStage.show();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

	public static void main(String[] args) {
		launch(args);
	}
}

```



Présentation 2

![](https://files.catbox.moe/50hiw5.jpg)

```java
...
public void start(Stage primaryStage) {
		try {
			StackPane root = new StackPane();
			Scene scene = new Scene(root,100,100);
			
      //JPG
			Rectangle helpIcon = new Rectangle(40,40);
			helpIcon.setFill(Color.CORNFLOWERBLUE);
      
      //Texte
			Text helpText = new Text("?");
			helpText.setFont(Font.font("Verdana", FontWeight.BOLD, 36));
			helpText.setFill(Color.WHITE);
			helpText.setStroke(Color.BLACK);
      
      //Ajouter 
			root.getChildren().addAll(helpIcon, helpText);
			//juste noeud helpIcon centré verticalement et aligné à droite
      
      //DIFF: Mettre helpicon au centre
			StackPane.setAlignment(helpIcon,Pos.CENTER_RIGHT); //所有元素在StackPane里面默认置中
      //Mettre tous les noeuds centrés verticalement et alignés à droite
			//DIFF:root.setAlignment(Pos.CENTER_RIGHT);
 
			StackPane.setMargin(helpText, new Insets(0, 10, 0, 0));
			//marge à droite

			primaryStage.setScene(scene);
			primaryStage.show();
		} catch (Exception e) {
			e.printStackTrace();
		}
}

...

```



### Partie 2 - GridPane

GridPane : noeuds répartis dans une grille

– Peuvent s’étendre sur plusieurs lignes/colonnes

– Grille pas forcément uniforme

​	• Largeur colonne →  largeur du noeud le plus large

​	• Hauteur ligne →  hauteur du noeud le plus haut

– Nb lignes /Nb colonnes déduits par place des noeuds

– Ajout d’un noeud n dans GridPane g

​	• `g.add(n, numCol, numLig, nbCol=1, nbLig=1)`	//把n放在numCol✖️numLig的第1列第1行

​	• numCol et numLig ≥ 0

​	• L’ordre d’ajout des noeuds n’a pas d’importance

– Si noeuds **dans même cellule** → superposition重叠

​	• Dernier ajouté → au-dessus



– Espacement(间隙)

​	• Horizontal des colonnes → `void setHgap(double v)`

​	• Vertical des lignes → `void setVgap(double v)`

– Visibilité de lignes de la grille → `void setGridLinesVisible(boolean b)`

​	• Très utile pour déboguer !

– Alignement de la grille dans son conteneur (位置)

​	• S’il y a de la place → `void setAlignment(Pos p)`

– Marge autour de la grille(与格子之间的边缘距离) → `void setPadding(Insets value)`



**Contraintes de placement**

​	– Globalement par ligne/colonne

​		• `getRowConstraints.add( )`

​		• `getColumnConstraint.add( )`

​		• L’ordre d’ajout = ordre ligne/colonne

​	![Expliquer](https://files.catbox.moe/xp2inr.png)

​	– Globalement par ligne/colonne

​		• `getRowConstraints.add( )`

​		• `getColumnConstraint.add( )`

​	– Par composant

​		• Prioritaires sur les contraintes globales

​		• Cf. méthodes statiques de GridPane



#### Exemple

![](https://files.catbox.moe/ohhmon.png)

![Eclipse résultat](https://files.catbox.moe/es0wp0.png)

```java
...
public void start(Stage primaryStage) {
		try {
			GridPane grid = new GridPane();
			grid.setHgap(5);	//H间隙为5
			grid.setVgap(10);	//V间隙为10
			grid.setGridLinesVisible(true);	//线条可见
      
      
			Scene scene = new Scene(grid, 200, 100);

      //Text
			Text titre1 = new Text("TITRE 1");
			grid.add(titre1, 0, 0);//放在第0列0行
			Text titre2 = new Text("TITRE 2");
			titre2.setFont(Font.font("Arial", FontWeight.BOLD, 20));
			grid.add(titre2, 0, 1);
      //Button
			Button b1 = new Button("Bouton 1");
			grid.add(b1, 1, 0, 1, 2);
			Button b2 = new Button("Bouton 2");
			GridPane.setHalignment(b2, HPos.CENTER); //Mettre b2 au centre(只是在对应格子里面的位置)
			grid.add(b2, 0, 2, 2, 1);	

			primaryStage.setScene(scene);
			primaryStage.show();
		} catch (Exception e) {
			e.printStackTrace();
		}
}
...
```

### Partie 3 - FlowPane

FlowPane : noeuds réparties

​	– sur une ligne horizontale (verticale)

​	– Passent à la ligne (colonne) suivante si plus de place

​	总之就是铺满一行或一列，然后自动转到下一行（列）

L’orientation est définie à la construction

![](https://files.catbox.moe/ge61pc.png)

– Ajout des noeuds dans FlowPane f

​	• `f.getChildren().add(node)`

​	• `f.getChildren().addAll(node1, node2, node3, …)`



![](https://files.catbox.moe/vsyn1v.png)

```java
...
public void start(Stage primaryStage) {
		try {
			FlowPane root = new FlowPane(Orientation.VERTICAL);
			Scene scene = new Scene(root,200,100);
			
			root.setPadding(new Insets(5, 0, 5, 0));
			root.setVgap(4);
			root.setHgap(4);
			root.setStyle("-fx-background-color: DAE6F3;");
			
			//Text
			Text titres[] = new Text[8];
			for (int i=0; i<8; i++) {	//Remplir la FlowPane
				titres[i] = new Text("Titre"+i);
				root.getChildren().add(titres[i]);	//IMP：Ajouter à la FlowPane
			}

			primaryStage.setScene(scene);
			primaryStage.show();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
...
```

### Partie 4 - TilePane

TilePane : les noeuds sont placés dans une grille (与FlowPane类似但是并不是所有格子（这里格子会自动铺满）大小都一样)

​	– Arrangement par colonne ou par ligne

​		• L’orientation est définie à la construction

​		• `Orientation.VERTICAL` ou `Orientation.HORIZONTAL`

​	– Le nombre de colonnes/lignes préférée est défini

​		• Juste pour calculer la taille préférée

​		• `setPrefColumns`,  `setPrefRow`

​		• Ne reflète pas forcément le nb de col ou lignes actuels

​	– Ajout des noeuds dans TilePane t

​		• `t.getChildren().add(node)`

​		• `t.getChildren().addAll(node1, node2, node3, …)`

#### Exemple

![](https://files.catbox.moe/asrgrx.png)

```java
...
public void start(Stage primaryStage) {
		try {
			TilePane root = new TilePane(Orientation.VERTICAL);
			Scene scene = new Scene(root,280,150);
			
			Text titres[] = new Text[4];
			Button bouton[] = new Button[4];
			for (int i=0; i<8; i++) {
				if (i%2==0){	//Texte 放在偶数的格子中
					titres[i/2] = new Text("Titre "+i/2);
					root.getChildren().add(titres[i/2]);
				}
				else{	//Bouton放在奇数的格子中
					bouton[i/2] = new Button("BOUTON "+i/2);
					root.getChildren().add(bouton[i/2]);
				}
			}
			bouton[2].setFont(Font.font("Arial", FontWeight.BOLD, 20));

			primaryStage.setScene(scene);
			primaryStage.show();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
...
```

### Partie 5 - AnchorPane(见PDF P22)

#### Exemple

![](https://files.catbox.moe/may0jj.png)

```java
public void start(Stage primaryStage) {
		try {
			AnchorPane root = new AnchorPane();
			Scene scene = new Scene(root,280,150);
			
			Button b[] = new Button[4];
			b[0]= new Button("Default");
			b[1]= new Button("Right");
			b[2]= new Button("LeftTop");
			b[3]= new Button("BottomLeftRight");
			

			root.getChildren().addAll(b[0],b[1],b[2],b[3]);
			AnchorPane.setRightAnchor(b[1], 20.0);	//老师写的有问题，这里往下的为Static方法
			AnchorPane.setLeftAnchor(b[2],60.0);
			AnchorPane.setTopAnchor(b[2],70.0);
			AnchorPane.setBottomAnchor(b[3],20.0);
			AnchorPane.setLeftAnchor(b[3],40.0);
			AnchorPane.setRightAnchor(b[3],40.0);
			

			primaryStage.setScene(scene);
			primaryStage.show();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
```



## 二 Modifications dans un conteneur(对Start里的更改)

**Suppression**

​	– Un noeud n à supprimer dans c

​		• `c.getChildren().remove(n)`

​	– Plusieurs noeuds à supprimer dans c

​		• `c.getChildren().removeAll(n1, n2, …)`

**Mettre à jour la fenêtre après modifications**

​	– `primaryStage.sizeToScene();`



## 三 Feuilles de style CSS (见PDF P24)



## 四 Boite de Dialog(P30)

### **3 types de boîtes**

​	– **Boîtes standard**

​		• Afficher un message › Alert

​		• Demander un choix ›TextInputDialog

​		• Saisir un texte › ChoiceDialog

​	– **Boîtes spécialisées, liées au système d’exploitation**

​		• Sélectionner des fichiers › FileChooser

​		• Sélectionner un répertoire › DirectoryChooser

​		• Sélectionner une date › DatePicker

​		• Sélectionner une couleur › ColorPicker

​	– **Boîtes personnalisées › cf. TP**



### 1. Boites standard

Définir une instance de la classe

Paramétrer la boîte

​	– Directement avec le constructeur

​	– Avec les méthodes set<XXX> de la classe

Afficher la boîte en mode modal →  `showAndWait()`

​	– Retourne le résultat éventuel de la boîte

​	– Bouton cliqué, texte saisi, texte choisi



#### 1.1 IMP：Alert

![](https://files.catbox.moe/2ynr4k.png)

```java
//...
public void start(Stage primaryStage) {
		try {
			
			Alert dialogA = new Alert(AlertType.WARNING);	//对应图标-感叹号
			//Alert dialogA = new Alert(AlertType.CONFIRMATION);	//图标-问号
			//Alert dialogA = new Alert(AlertType.ERROR);	//图标-错误
			ButtonType bAide = new ButtonType ("Aide", ButtonData.HELP);
			dialogA.getButtonTypes().setAll(ButtonType.OK, bAide);
			dialogA.setTitle("Avertissement");
			dialogA.setHeaderText("Gestion de la batterie");
			//dialogA.setHeaderText(null); // IMP：简化抬头
			dialogA.setContentText("Attention : vos batteries sont faibles !");
			
			Optional<ButtonType> reponse = dialogA.showAndWait();
      
			if (reponse.get() == ButtonType.OK)
				System.out.println("Bouton OK choisi");
			else //if (reponse.get() == bAide)
				System.out.println("Bouton Aide choisi");
			

		} catch (Exception e) {
			e.printStackTrace();
		}
	}
//...
```

#### 1.2 IMP：TextInputDialog

![](https://files.catbox.moe/m822b7.png)

```java
//...
public void start(Stage primaryStage) {
		try {
			
			TextInputDialog boiteTxt = new TextInputDialog("Valeur par défaut");
			boiteTxt.setTitle("Une boîte pour saisir du texte");
			boiteTxt.setHeaderText("Gestion des noms des utilisateurs");
			boiteTxt.setContentText("Votre nom :");
			
			Optional<String> text = boiteTxt.showAndWait();
			
			if (text.isPresent())
				System.out.println("Votre nom est = " + text.get()); 
			

		} catch (Exception e) {
			e.printStackTrace();
		}
	}
//...
```

#### 1.3 ChoiceDialog

![](https://files.catbox.moe/cvto82.png)

```java
	public void start(Stage primaryStage) {
		try {
			String[] choix = {"Urgent", "Elevé", "Standard", "Faible"};	//设置选项
			ChoiceDialog<String> boiteChoix = new ChoiceDialog<>(choix[2], choix);
			
			boiteChoix.setTitle("Une boîte pour faire un choix");
			boiteChoix.setHeaderText("Sélectionnez la priorité d'exécution");
			boiteChoix.setContentText("Priorité:");
			
			Optional<String> selection = boiteChoix.showAndWait();
			
			if (selection.isPresent())
				System.out.println("Votre choix de priorité est = " + selection.get());
			
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
```

## 五 Gestion des événements - Répondre aux actions de l’utilisateur (P34)





#### Button Add - p42

```java
AddButton.addEventHandler(ActionEvent.ACTION,
new EventHandler<ActionEvent>() {
@Override
public void handle(ActionEvent event) {
TextInputDialog inDialog = new TextInputDialog("");
inDialog.setTitle("Saisissez un texte");
inDialog.setHeaderText(null);
inDialog.setContentText("Votre texte :");
  
Optional<String> textIn = inDialog.showAndWait();
if (textIn.isPresent() && !textIn.get().isEmpty()) {
	list.getItems().add(textIn.get());
}
});
```

#### Button Delete - p43(Dans un autre Class)

用法：

```java
DelButtonController delBC = new DelButtonController(list);
DelButton.addEventHandler(ActionEvent.ACTION, delBC);	//向名为DelButton的按钮添加删除功能
```



```java
public class DelButtonController implements
EventHandler<ActionEvent> {
ListView<String> _list;
public DelButtonController(ListView<String> list){
this._list = list; }
@Override
public void handle(ActionEvent event) {
ObservableList<Integer> selectedIndices =
_list.getSelectionModel().getSelectedIndices();
for (int i= selectedIndices.size()-1;i>=0;i--) {
int indice = selectedIndices.get(i).intValue();
_list.getItems().remove(indice);
}}}
```



#### Button Clear p44

```java
ClearButton.setOnAction(new EventHandler<ActionEvent>(){
@Override
public void handle(ActionEvent event) {
list.getItems().clear();
}
});
```

​	2ième Méthode: utiliser une expression lambda

```java
ClearButton.setOnAction(event->{list.getItems().clear();});
```



#### 更新DeleteButton状态

```java
list.getSelectionModel().selectedItemProperty().addListener(
(observable, oldValue, newValue) -> { DelButton.setDisable(	//IMP
list.getSelectionModel().getSelectedItems().size()== 0);}
);
```



#### 滚动条p48