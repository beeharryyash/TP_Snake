# Snake game.
#### A readme is been made so as users can easily know how to execute the game.

## Prerequisites.
##### This section indicates what are the requirements that should be poccessed in order to be able to start.
 - esclipse workspace
 - JavaFX SDK, Which should be downloaded from the website GluonHQ or from the link below directly.
 ```sh 
  https :://gluonhq.com/products/javafx/ 
```

## Set up.
##### The steps found below will helps to configure a project properly before starting the coding part. 

- we first create a java project with the name SnakeGame
- Once the project is created we need to configure the build path, To do so follow the steps below.

##### Steps
 ```sh 
  Right click on the project which has been created.

 Click on build path -> Configure build path -> Libraries -> Module path -> Add External JARS
  
  Once add External JARS is been click, a JARS selection page will pop up
  Select all the librabies found in the Folder lib.
    openjfx-21.0.2_windows-x64_bin-sdk -> javafx-sdk-21.0.2 -> lib
    
Once all libraries is been selected, click on apply and close, A new file name 
`Reference libraries` will be created in the project file which will contained all the
libraries which have been selected.
```

#### After the above steps has been successfully been done we may proceed with the remaining procedures.

##### Creation of a new package.
 ```sh 
    Create a new package as follows:
    com.[your name].SnakeFX
        example: com.toto.SnakeFX

Upon successful creation it will appear in the SRC folder
```

##### Creation of a new class.
 ```sh 
    Create a new class as follows:
        example: SnakeApp
Make sure that public static void main(string[]arg) is been selected during the creation.
```


##### Once the class is been created we will need to run the configurations.
 ```sh 
 click on run -> run configurations
 Select the snakeGame project in the main section
 
 And then we need to set the vm arguments which is found in the argument section.
 --module-path "THE PATH OF THE LIB FOLDER WHICH IS FOUND IN THE JAVAFX_SDK WHICH HAS 
 BEEN DOWNLOADED" --add-modules javafx.controls,javafx.fxml
 
 EXAMPLE:
 --module-path "C:\Users\toto\Downloads\openjfx-21.0.2_windows-x64_bin-sdk\javafx-sdk-21.0.2
 \lib" --add-modules javafx.controls,javafx.fxml


 Once done apply and run.
```


##### Creation of the game.
 ```sh 
    Copy and paste the code found in the Sourcecode file and paste it in 
    the SnakeApp.jave file

    Once copy, save and run the project.
```


##### How to play the game.
 ```sh 
    To move the snake simply use the direction key. Each time a food is been eat the snake 
    will increase in size. If the snake passes onto itself the user losses and the game
    will be over.
```
