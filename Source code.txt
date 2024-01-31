package com.beeharry.SnakeFX;

import javafx.animation.AnimationTimer;
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.canvas.Canvas;
import javafx.scene.canvas.GraphicsContext;
import javafx.scene.layout.StackPane;
import javafx.scene.paint.Color;
import javafx.scene.text.Font;
import javafx.stage.Stage;

import java.util.ArrayList;
import java.util.List;
import java.util.Random;

public class SnakeApplication extends Application {

    private static final int TILE_SIZE = 20;
    private static final int WIDTH = 20;
    private static final int HEIGHT = 20;

    private List<Position> snake;
    private Direction direction = Direction.RIGHT;
    private boolean gameOver = false;
    private Position food;
    private int score = 0;

    @Override
    public void start(Stage primaryStage) {
        Canvas canvas = new Canvas(WIDTH * TILE_SIZE, HEIGHT * TILE_SIZE);
        GraphicsContext gc = canvas.getGraphicsContext2D();
        snake = new ArrayList<>();
        snake.add(new Position(WIDTH / 2, HEIGHT / 2));
        spawnFood();

        StackPane root = new StackPane(canvas); // Create a StackPane
        root.setStyle("-fx-background-color: black;"); // Set background color to black
        Scene scene = new Scene(root);

        new AnimationTimer() {
            long lastUpdate = 0;

            @Override
            public void handle(long now) {
                if (now - lastUpdate >= 1000000000 / 5) {
                    lastUpdate = now;
                    if (!gameOver) {
                        update();
                        draw(gc);
                    } else {
                        stop();
                    }
                }
            }
        }.start();

        scene.setOnKeyPressed(event -> {
            switch (event.getCode()) {
                case UP:
                    direction = Direction.UP;
                    break;
                case DOWN:
                    direction = Direction.DOWN;
                    break;
                case LEFT:
                    direction = Direction.LEFT;
                    break;
                case RIGHT:
                    direction = Direction.RIGHT;
                    break;
            }
        });

        primaryStage.setScene(scene);
        primaryStage.setTitle("Snake Game");
        primaryStage.show();
    }

    private void update() {
        Position head = snake.get(0);
        Position newHead = new Position(head.getX(), head.getY());
        switch (direction) {
            case UP:
                newHead.setY((newHead.getY() - 1 + HEIGHT) % HEIGHT); // Wrap around the top edge
                break;
            case DOWN:
                newHead.setY((newHead.getY() + 1) % HEIGHT); // Wrap around the bottom edge
                break;
            case LEFT:
                newHead.setX((newHead.getX() - 1 + WIDTH) % WIDTH); // Wrap around the left edge
                break;
            case RIGHT:
                newHead.setX((newHead.getX() + 1) % WIDTH); // Wrap around the right edge
                break;
        }
        if (newHead.equals(food)) {
            snake.add(0, newHead);
            spawnFood();
            score++; // Increase score when the snake eats food
        } else {
            snake.add(0, newHead);
            snake.remove(snake.size() - 1);
        }
        if (snake.stream().skip(1).anyMatch(newHead::equals)) { // Check if snake collides with itself
            gameOver = true;
        }
    }

    private void draw(GraphicsContext gc) {
        gc.clearRect(0, 0, WIDTH * TILE_SIZE, HEIGHT * TILE_SIZE);
        gc.setFill(Color.GREEN);
        snake.forEach(p -> gc.fillRect(p.getX() * TILE_SIZE, p.getY() * TILE_SIZE, TILE_SIZE, TILE_SIZE));
        gc.setFill(Color.RED);
        gc.fillRect(food.getX() * TILE_SIZE, food.getY() * TILE_SIZE, TILE_SIZE, TILE_SIZE);
        gc.setFill(Color.WHITE);
        gc.setFont(new Font("Arial", 20));
        gc.fillText("Score: " + score, 10, 20); // Display score
        if (gameOver) {
            gc.setFill(Color.WHITE);
            gc.fillText("Game Over!", 50, 100);
        }
    }

    private void spawnFood() {
        Random random = new Random();
        int x = random.nextInt(WIDTH);
        int y = random.nextInt(HEIGHT);
        food = new Position(x, y);
        while (snake.contains(food)) {
            x = random.nextInt(WIDTH);
            y = random.nextInt(HEIGHT);
            food = new Position(x, y);
        }
    }

    public static void main(String[] args) {
        launch(args);
    }

    private static class Position {
        private int x;
        private int y;

        public Position(int x, int y) {
            this.x = x;
            this.y = y;
        }

        public int getX() {
            return x;
        }

        public void setX(int x) {
            this.x = x;
        }

        public int getY() {
            return y;
        }

        public void setY(int y) {
            this.y = y;
        }

        public boolean equals(Position other) {
            return this.x == other.x && this.y == other.y;
        }
    }

    private enum Direction {
        UP, DOWN, LEFT, RIGHT
    }
}

