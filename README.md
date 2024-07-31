# TicTacToe
package tictactao_project;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TicTacToe extends JFrame {
    private JButton[][] buttons = new JButton[3][3];
     
      
    private boolean xTurn = true;

    public TicTacToe() {
        setTitle("Tic-Tac-Toe");
        setSize(300, 300);
        setLayout(new GridLayout(3, 3));
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        initializeButtons();
    }

    private void initializeButtons() {
        ActionListener buttonListener = new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                JButton button = (JButton) e.getSource();
                if (button.getText().equals("") && !isGameOver()) {
                    button.setText(xTurn ? "X" : "O");
                    xTurn = !xTurn;
                    if (checkForWin()) {
                        JOptionPane.showMessageDialog(null, (xTurn ? "O" : "X") + " WIN !");
                    } else if (isBoardFull()) {
                        JOptionPane.showMessageDialog(null, "It's a draw!");
                    }
                }
            }
        };

        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                buttons[i][j] = new JButton("");
                buttons[i][j].setFont(new Font("Arial", Font.ITALIC, 60));
                buttons[i][j].setFocusPainted(false);
                buttons[i][j].addActionListener(buttonListener);
                add(buttons[i][j]);
            }
        }
        buttons[0][0].setBackground(Color.RED);
        buttons[0][1].setBackground(Color.RED);
        buttons[0][2].setBackground(Color.RED);
        buttons[1][0].setBackground(Color.RED);
        buttons[1][1].setBackground(Color.RED);
        buttons[1][2].setBackground(Color.RED);
        buttons[2][0].setBackground(Color.RED);
        buttons[2][1].setBackground(Color.RED);
        buttons[2][2].setBackground(Color.RED);
    }

    private boolean checkForWin() {
        // Check rows
        for (int i = 0; i < 3; i++) {
            if (buttons[i][0].getText().equals(buttons[i][1].getText()) &&
                buttons[i][1].getText().equals(buttons[i][2].getText()) &&
                !buttons[i][0].getText().equals("")) {
                return true;
            }
        }

        // Check columns
        for (int i = 0; i < 3; i++) {
            if (buttons[0][i].getText().equals(buttons[1][i].getText()) &&
                buttons[1][i].getText().equals(buttons[2][i].getText()) &&
                !buttons[0][i].getText().equals("")) {
                return true;
            }
        }

        // Check diagonals
        if (buttons[0][0].getText().equals(buttons[1][1].getText()) &&
            buttons[1][1].getText().equals(buttons[2][2].getText()) &&
            !buttons[0][0].getText().equals("")) {
            return true;
        }

        if (buttons[0][2].getText().equals(buttons[1][1].getText()) &&
            buttons[1][1].getText().equals(buttons[2][0].getText()) &&
            !buttons[0][2].getText().equals("")) {
            return true;
        }

        return false;
    }

    private boolean isBoardFull() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (buttons[i][j].getText().equals("")) {
                    return false;
                }
            }
        }
        return true;
    }

    private boolean isGameOver() {
        return checkForWin() || isBoardFull();
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            TicTacToe game = new TicTacToe();
            game.setVisible(true);
        });
    }
}
