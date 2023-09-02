import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Alert;
import javafx.scene.control.Alert.AlertType;
import javafx.scene.control.TextField;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;

public class SudokuGUI extends Application {
    private int[][] board = new int[9][9];
    private TextField[][] textFields = new TextField[9][9];

    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        initializeBoard();

        GridPane grid = new GridPane();
        grid.setHgap(5);
        grid.setVgap(5);

        for (int row = 0; row < 9; row++) {
            for (int col = 0; col < 9; col++) {
                int value = board[row][col];
                textFields[row][col] = new TextField(value == 0 ? "" : String.valueOf(value));
                textFields[row][col].setPrefWidth(40);
                textFields[row][col].setPrefHeight(40);
                textFields[row][col].setStyle("-fx-font-size: 18;");
                grid.add(textFields[row][col], col, row);
            }
        }

        Scene scene = new Scene(grid, 400, 400);
        primaryStage.setTitle("Sudoku");
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    private void initializeBoard() {
        // Initialize the Sudoku board. You can replace this with your own Sudoku puzzle.
        // Use 0 to represent empty cells.
        int[][] initialBoard = {
            {5, 3, 0, 0, 7, 0, 0, 0, 0},
            {6, 0, 0, 1, 9, 5, 0, 0, 0},
            {0, 9, 8, 0, 0, 0, 0, 6, 0},
            {8, 0, 0, 0, 6, 0, 0, 0, 3},
            {4, 0, 0, 8, 0, 3, 0, 0, 1},
            {7, 0, 0, 0, 2, 0, 0, 0, 6},
            {0, 6, 0, 0, 0, 0, 2, 8, 0},
            {0, 0, 0, 4, 1, 9, 0, 0, 5},
            {0, 0, 0, 0, 8, 0, 0, 7, 9}
        };

        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                board[i][j] = initialBoard[i][j];
            }
        }
    }
}
public class SudokuSolver {
    private int[][] board;
 public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        initializeBoard();

        while (!isSudokuSolved()) {
            printBoard();
            System.out.print("Enter row (1-9), column (1-9), and value (1-9) separated by spaces (e.g., '3 4 6'): ");
            int row = scanner.nextInt() - 1;
            int col = scanner.nextInt() - 1;
            int value = scanner.nextInt();

            if (isValidMove(row, col, value)) 
                board[row][col] = value;
         else 
                System.out.println("Invalid move! Try again.");
            }
            
        }
        

        System.out.println("Congratulations! You've solved the Sudoku puzzle.");
        printBoard();
        scanner.close();
    }
    public SudokuSolver(int[][] board) {
        this.board = board;
    }

    public boolean solve() {
        
        return false; 
    }

    public int[][] getBoard() {
        return board;
    }
 private static boolean isSudokuSolved() {
        // Check if the Sudoku puzzle is solved (no empty cells).
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == 0) {
                    return false;
                }
            }
        }
        return true;
    }
  private static void printBoard() {
        System.out.println("Sudoku Board:");
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                System.out.print(board[i][j] + " ");
                if (j == 2 || j == 5) {
                    System.out.print("| ");
                }
            }
            System.out.println();
            if (i == 2 || i == 5) {
                System.out.println("---------------------");
            }
        }
        System.out.println();
    }
    
}
