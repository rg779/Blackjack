# Blackjack
Blackjack game created summer 2020

*main class*
import java.util.Scanner;
public class Game {

	public static void main(String[] args) {
		
		Scanner in = new Scanner(System.in);
		
		// variables
		boolean playing = true;
		int total = 0;
		String cards = "";
		Card current = null;
		String decision = "";
		
		// bot variables
		int botTotal = 0;
		
		// introduction
		System.out.println("Welcome to Blackjack!");
		Deck blackjack = new Deck();
		
		// initialization
		current = blackjack.getCard();
		System.out.println("You drew a " + current.getName());
		cards += current.getName();
		System.out.println("Cards: " + cards);
		total += current.getValue();
		System.out.println("Total: " + total);
		
		botTotal += blackjack.getCard().getValue();
		
		// game loop
		do {
		System.out.println("Would you like to hit or stay? Enter h or s");
		decision = in.next();
		if (decision.equals("h")) {
			current = blackjack.getCard();
			System.out.println("You drew a " + current.getName());
			cards += ", " + current.getName();
			System.out.println("Cards: " + cards);
			total += current.getValue();
			System.out.println("Total: " + total);
			
			botTotal += blackjack.getCard().getValue();
		} else if (decision.equals("s")) {
			playing = false;
		}
		if (total >= 21) {
			playing = false;
		}
		
		} while (playing == true); // game ends
		
		// evaluation 
		if (total > 21) {
			System.out.println("You went over 21. You lost!");
		} else if (total == 21) {
			System.out.println("You reached 21. You won!");
		} else {
			if (botTotal > 21) {
				System.out.println("Your opponent went over 21. You won!");
			} else if (total > botTotal) {
				System.out.println("You had " + total + ". Your opponent had " + botTotal + ". You won!");
			} else if (total < botTotal) {
				System.out.println("You had " + total + ". Your opponent had " + botTotal + ". You lost!");
			} else {
				System.out.println("Something went wrong :( Please try again.");
			}
		}

	}

}
------------------------------------------------------------------
*supporting classes*
import java.util.ArrayList;
import java.math.*;

public class Deck {

	private ArrayList <Card> collection;
	int r = 0;
	public Deck() {
		collection = new ArrayList <Card>();
		for (int i = 1; i <= 13; i++) {
			collection.add(new Card(i));
		}
	}
	public Card getCard() {
		r = (int)(Math.random() * (collection.size() + 1));
		return collection.get(r);
		
	}
	

}
------------------------------------------------------------------

public class Card {

	private int value = 0;
	
	public Card(int num) {
		value = num;
	}
	public int getValue() {
		return value;
	}
	public String getName() {
		if (value < 11) {
			return "" + value;
		} else if (value == 11) {
			return "J";
		} else if (value == 12) {
			return "Q";
		} else if (value == 13) {
			return "K";
		} else {
			return "error";
		}
	}
}

