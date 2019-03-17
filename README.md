//# BrownGuy
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import java.applet.Applet;

public class TwentyOneGame extends Applet implements ActionListener
{
	Panel p_card;  //to hold all of the screens
	Panel card1, card2, card3, card4, card5; //the two screens
	CardLayout cdLayout = new CardLayout ();
	JLabel bet, balance, points;
	int PLbalance = 500;
  int cardN;
	int cardS;
	int Ppoints = 0;
	int Dpoints = 0;
	JButton hit, stand;

	//grid
	int row = 2;
	int col = 5;
	JLabel a[]  = new JLabel [row * col];
	int b[] [] = {
			{1, 2, 1, 2, 1},{1,1,1,1,1}};

	int row1 = 2;
	int col1 = 5;
	//JLabel c[] = new JLabel [row1 * col1];
	char d [] [] = {
			{'b', ' ', 'b', ' ', 'b'},
			{' ', 'b', ' ', 'b', ' '}};

	public void init ()
	{
		p_card = new Panel ();
		p_card.setLayout (cdLayout);
		screen1 ();
		screen2 ();
		screen3 ();
		screen4 ();
		screen5 ();
		resize (500, 600);
		setLayout (new BorderLayout ());
		add ("Center", p_card);
	}


	public void screen1 ()
	{ //screen 1 is set up.
		card1 = new Panel ();
		card1.setBackground (Color.white);
		JButton next = new JButton (createImageIcon("BJtitle.png"));
		next.setActionCommand ("s2");
		next.addActionListener (this);
		card1.add (next);
		p_card.add ("1", card1);
	}


	public void screen2 ()
	{ //screen 2 is set up.
		card2 = new Panel ();
		card2.setBackground (Color.orange);
		//JLabel title = new JLabel (createImageIcon("BJints.png"));
		JButton next = new JButton (createImageIcon("BJints.png"));
		next.setActionCommand ("s3");
		next.addActionListener (this);
		//card2.add (title);
		card2.add (next);
		p_card.add ("2", card2);
	}


	public void screen3 ()
	{ //screen 3 is set up.
		card3 = new Panel ();
		card3.setBackground (new Color (1 ,69, 28));
		JLabel title = new JLabel (createImageIcon("BJplainTit.png"));
		JButton next = new JButton ("Next");
		next.setActionCommand ("s4");
		next.addActionListener (this);



		//Set up grid

		Panel cd = new Panel (new GridLayout (row, col));
		int move1 = 0;
		for (int i = 0 ; i < row ; i++)
		{
			for (int j = 0 ; j < col ; j++)
			{ //take out when you've got pictures
				//c [move1] = new JLabel ("");
				//add in when you have pictures
				a [move1] = new JLabel (createImageIcon ("red_back" + d [i] [j] + ".png"));
				a [move1].setPreferredSize (new Dimension (50, 75));
				//				c [move1].addActionListener (this);
				//			c [move1].setActionCommand ("" + move1);
				cd.add (a [move1]);
				move1++;
			}
		}

		Panel p = new Panel (new GridLayout (row, col));
		int move = 0;
		for (int i = 0 ; i < row ; i++)
		{
			for (int j = 0 ; j < col ; j++)
			{ //take out when you've got pictures
				//a [move] = new JLabel ("");
				//add in when you have pictures
				a [move] = new JLabel (createImageIcon (b [i] [j] + ".jpg"));
				a [move].setPreferredSize (new Dimension (80, 118));
				//a [move].addActionListener (this);
				//a [move].setActionCommand ("" + move);
				p.add (a [move]);
				move++;
			}
		}
		//DealersCards();
		
		Panel chips = new Panel (new GridLayout (1,5));
		chips.setPreferredSize(new Dimension (300,50));

		JButton fifty = new JButton ("$50");
		fifty.setActionCommand ("50");
		fifty.addActionListener (this);

		JButton t5 = new JButton ("$25");
		t5.setActionCommand ("25");
		t5.addActionListener (this);
		JButton ten = new JButton ("$10");
		ten.setActionCommand ("10");
		ten.addActionListener (this);
		JButton five = new JButton ("$5");
		five.setActionCommand ("5");
		five.addActionListener (this);
		JButton one = new JButton ("$1");
		one.setActionCommand ("1");
		one.addActionListener (this);
		chips.add(fifty);
		chips.add(t5);
		chips.add(ten);
		chips.add(five);
		chips.add(one);
		Panel clickables = new Panel (new GridLayout (1,3));
		//clickables.setPreferredSize(new Dimension (245,50));
		hit = new JButton ("Hit");
		hit.setActionCommand ("hit");
		hit.addActionListener (this);
		hit.setEnabled(false);
		hit.setPreferredSize(new Dimension (90,50));
		bet = new JLabel ("You Bet:");
		bet.setForeground(Color.white);
		stand = new JButton ("Stand");
		stand.setActionCommand ("stand");
		stand.setEnabled(false);
		stand.addActionListener (this);
		clickables.add(hit);
		clickables.add(bet);
		clickables.add(stand);
		Panel BlanceOnsCREEN = new Panel (new GridLayout (1,3));
		BlanceOnsCREEN.setPreferredSize(new Dimension(245,50));
		points = new JLabel ("Player Points:"+Ppoints);
		points.setForeground(Color.white);

		balance = new JLabel ("Your Balance: "+PLbalance);
		balance.setForeground(Color.white);

		BlanceOnsCREEN.add(balance);
		BlanceOnsCREEN.add(points);
		card3.add (title);
		card3.add (cd);
		card3.add (clickables);
		card3.add (p);
		card3.add(chips);
		card3.add (BlanceOnsCREEN);
		//card3.add (next);
		p_card.add ("3", card3);
	}

	/*public void DealersCards() {
		cardN = (int) + (Math.random () * 10 + 1);
		cardS = (int) + (Math.random () * 4 + 1);
		if(cardS == 1) {
			Dpoints += cardN;
			c[1].setText(cardN+" of Diamonds");
			c[1].setForeground(Color.white);
		}
		else if(cardS == 2) {
			Dpoints += cardN;
			c[2].setText(cardN+" of Hearts");
			c[2].setForeground(Color.white);
		}
		else if(cardS == 3) {
			Dpoints += cardN;
			c[3].setText(cardN+" of Clubs");
			c[3].setForeground(Color.white);
		}
		else if(cardS == 4) {
			Dpoints += cardN;
			c[4].setText(cardN+" of Spades");
			c[4].setForeground(Color.white);
		}
	}

*/

	public void PlayersCards() {
		cardN = (int) + (Math.random () * 10 + 1);
		cardS = (int) + (Math.random () * 4 + 1);
		if(cardS == 1) {
			if(Ppoints < 50) {
				Ppoints += cardN;
				points.setText("Player points: "+Ppoints);
				thing();
			}

			else if (Ppoints > 50)
				JOptionPane.showMessageDialog(null, "POINTS EXCEEDEd");
		}
		else if(cardS == 2) {
			if(Ppoints < 50) {
				Ppoints += cardN;
				points.setText("Player points: "+Ppoints);
				thing();
			}

			else if (Ppoints > 50)
				JOptionPane.showMessageDialog(null, "POINTS EXCEEDEd");
		}
		else if(cardS == 3) {
			if(Ppoints < 50) {
				Ppoints += cardN;
				points.setText("Player points: "+Ppoints);
				thing();
			}

			else if (Ppoints > 50)
				JOptionPane.showMessageDialog(null, "POINTS EXCEEDEd");
		}

		else if(cardS == 4) {
			if(Ppoints < 50) {
				Ppoints += cardN;
				points.setText("Player points: "+Ppoints);
				thing();
			}

			else if (Ppoints > 50)
				JOptionPane.showMessageDialog(null, "POINTS EXCEEDEd");			
		}
	}

	public void thing1 () {
		if (cardN == 1 && cardS == 1) 
			b[0][1] = 'b';
		showStatus("WORKS");
			/*else if (cardN == 1 && cardS == 2)
				a[0].setIcon (createImageIcon ("p7.png"));
			else if (cardN == 1 && cardS == 3)
				a[0].setIcon (createImageIcon ("p1.png"));
			else if (cardN == 1 && cardS == 4)
				a[0].setIcon (createImageIcon ("p8.png"));
		*/
		
		if (cardN == 2 )
			a[1].setIcon (createImageIcon ("p7.png"));
		if (cardN == 3 )
			a[2].setIcon (createImageIcon ("p1.png"));
		if (cardN == 4 )
			a[3].setIcon (createImageIcon ("p8.png"));
		if (cardN == 5 )
			a[4].setIcon (createImageIcon ("p3.png"));
		if (cardN == 6 )
			a[5].setIcon (createImageIcon ("p4.png"));
		if (cardN == 7 )
			a[6].setIcon (createImageIcon ("p5.png"));
		if (cardN == 8 )
			a[7].setIcon (createImageIcon ("p11.png"));
		if (cardN == 9 )
			a[8].setIcon (createImageIcon ("p12.png"));
		if (cardN == 10 )
			a[9].setIcon (createImageIcon ("p20.png"));


	}
	
	public void thing () {

		/*if (cardN == 2 && cardS == 1) {
			a[0][1].setIcon(createImageIcon("2Hearts.png"));
		showStatus("WORKS");}
			else if (cardN == 2 && cardS == 2)
				a[1].setIcon (createImageIcon ("2Clubs.png"));
			else if (cardN == 2 && cardS == 3)
				a[1].setIcon (createImageIcon ("2Diamonds.png"));
			else if (cardN == 2 && cardS == 4)
				a[1].setIcon (createImageIcon ("2Hearts.png"));
		
		
		if (cardN == 1 )
			a[0].setIcon (createImageIcon ("2Hearts.png"));
		if (cardN == 3 )
			a[2].setIcon (createImageIcon ("2Diamonds.png"));
		if (cardN == 4 )
			a[3].setIcon (createImageIcon ("2Clubs.png"));
		if (cardN == 5 )
			a[4].setIcon (createImageIcon ("2Ace.png"));
		if (cardN == 6 )
			a[5].setIcon (createImageIcon ("p4.png"));
		if (cardN == 7 )
			a[6].setIcon (createImageIcon ("p5.png"));
		if (cardN == 8 )
			a[7].setIcon (createImageIcon ("p11.png"));
		if (cardN == 9 )
			a[8].setIcon (createImageIcon ("p12.png"));
		if (cardN == 10 )
			a[9].setIcon (createImageIcon ("p20.png"));

	
		/*	else if (cardS == 2 && cardN == 2)
			a[1].setIcon (createImageIcon ("p7.png"));
		else if (cardS == 2 && cardN == 3)
			a[1].setIcon (createImageIcon ("p1.png"));
		else if (cardS == 2 && cardN == 4)
			a[1].setIcon (createImageIcon ("p8.png"));

		if (cardS == 3 && cardN == 1) 
			showStatus("2");
		else if (cardS == 3 && cardN == 2)
			a[2].setIcon (createImageIcon ("p7.png"));
		else if (cardS == 3 && cardN == 3)
			a[2].setIcon (createImageIcon ("p1.png"));
		else if (cardS == 3 && cardN == 4)
			a[2].setIcon (createImageIcon ("p8.png"));

		if (cardS == 4 && cardN == 1) 
			showStatus("2");
		else if (cardS == 4 && cardN == 2)
			a[3].setIcon (createImageIcon ("p7.png"));
		else if (cardS == 4 && cardN == 3)
			a[3].setIcon (createImageIcon ("p1.png"));
		else if (cardS == 4 && cardN == 4)
			a[3].setIcon (createImageIcon ("p8.png"));

		if (cardS == 5 && cardN == 1) 
		showStatus("2");
		else if (cardS == 5 && cardN == 2)
			a[4].setIcon (createImageIcon ("p7.png"));
		else if (cardS == 5 && cardN == 3)
			a[4].setIcon (createImageIcon ("p1.png"));
		else if (cardS == 5 && cardN == 4)
			a[4].setIcon (createImageIcon ("p8.png"));

		if (cardS == 6 && cardN == 1) 
	showStatus("2");
		else if (cardS == 6 && cardN == 2)
			a[5].setIcon (createImageIcon ("p7.png"));
		else if (cardS == 6 && cardN == 3)
			a[5].setIcon (createImageIcon ("p1.png"));
		else if (cardS == 6 && cardN == 4)
			a[5].setIcon (createImageIcon ("p8.png"));

		if (cardS == 7 && cardN == 1) 
			showStatus("2");
		else if (cardS == 7 && cardN == 2)
			a[6].setIcon (createImageIcon ("p7.png"));
		else if (cardS == 7 && cardN == 3)
			a[6].setIcon (createImageIcon ("p1.png"));
		else if (cardS == 7 && cardN == 4)
			a[6].setIcon (createImageIcon ("p8.png"));

		if (cardS == 8 && cardN == 1) 
	showStatus("8");
		else if (cardS == 8 && cardN == 2)
			a[7].setIcon (createImageIcon ("p7.png"));
		else if (cardS == 8 && cardN == 3)
			a[7].setIcon (createImageIcon ("p1.png"));
		else if (cardS == 8 && cardN == 4)
			a[7].setIcon (createImageIcon ("p8.png"));

		if (cardS == 9 && cardN == 1) 
			showStatus("9");
		else if (cardS == 9 && cardN == 2)
			a[8].setIcon (createImageIcon ("p7.png"));
		else if (cardS == 9 && cardN == 3)
			a[8].setIcon (createImageIcon ("p1.png"));
		else if (cardS == 9 && cardN == 4)
			a[8].setIcon (createImageIcon ("p8.png"));

		if (cardS == 10 && cardN == 1) 
	showStatus("10");
		else if (cardS == 10 && cardN == 2)
			a[9].setIcon (createImageIcon ("p7.png"));
		else if (cardS == 10 && cardN == 3)
			a[9].setIcon (createImageIcon ("p1.png"));
		else if (cardS == 10 && cardN == 4)
			a[9].setIcon (createImageIcon ("p8.png"));
		/*
		else if (cardN == 2) {
			a[1].setText(cardN+" of "+cardS);
			a[1].setForeground(Color.white);
		}

		else if (cardN == 3) {
			a[2].setText(cardN+" of "+cardS);
			a[2].setForeground(Color.white);
		}

		else if (cardN == 4) {
			a[3].setText(cardN+" of "+cardS);
			a[3].setForeground(Color.white);
		}

		else if (cardN == 5) {
			a[4].setText(cardN+" of "+cardS);
			a[4].setForeground(Color.white);
		}

		else if (cardN == 6) {
			a[5].setText(cardN+" of "+cardS);
			a[5].setForeground(Color.white);
		}

		else if (cardN == 7) {
			a[6].setText(cardN+" of "+cardS);
			a[6].setForeground(Color.white);
		}

		else if (cardN == 8) {
			a[7].setText(cardN+" of "+cardS);
			a[7].setForeground(Color.white);
		}

		else if (cardN == 9) {
			a[8].setText(cardN+" of "+cardS);
			a[8].setForeground(Color.white);
		}

		else if (cardN == 10) {
			a[9].setText(cardN+" of "+cardS);
			a[9].setForeground(Color.white);
		}
		 */
	}


	public void screen4 ()
	{ //screen 4 is set up.
		card4 = new Panel ();
		card4.setBackground (Color.yellow);
		JLabel title = new JLabel ("You Win!");
		JButton next = new JButton ("Next");
		next.setActionCommand ("s5");
		next.addActionListener (this);
		card4.add (title);
		card4.add (next);
		p_card.add ("4", card4);
	}


	public void screen5 ()
	{ //screen 5 is set up.
		card5 = new Panel ();
		card5.setBackground (Color.cyan);
		JLabel title = new JLabel ("You Lose.");
		JButton next = new JButton ("Back to Introduction?");
		next.setActionCommand ("s1");
		next.addActionListener (this);
		JButton end = new JButton ("Quit?");
		end.setActionCommand ("s6");
		end.addActionListener (this);
		card5.add (title);
		card5.add (next);
		card5.add (end);
		p_card.add ("5", card5);
	}


	protected static ImageIcon createImageIcon (String path)
	{ //change the red to your class name
		java.net.URL imgURL = TwentyOneGame.class.getResource (path);
		if (imgURL != null)
		{
			return new ImageIcon (imgURL);
		}
		else
		{
			System.err.println ("Couldn't find file: " + path);
			return null;
		}
	}


	public void redraw ()
	{
		int move = 0;
		for (int i = 0 ; i < row ; i++)
		{
			for (int j = 0 ; j < col ; j++)
			{
				a [move].setIcon (createImageIcon (b [i] [j] + ".jpg"));
				move++;
			}
		}
	}

	public void belowBetStop () {
		if (PLbalance <= 0) {
			PLbalance = 0;
			JOptionPane.showMessageDialog(null, "Not enough money to bet");
			balance.setText("Your balamce: ---");
		}
		else 
			showStatus("BETTING");

	}

	public void actionPerformed (ActionEvent e)
	{ //moves between the screens
		if (e.getActionCommand ().equals ("s1"))
			cdLayout.show (p_card, "1");
		else if (e.getActionCommand ().equals ("s2"))
			cdLayout.show (p_card, "2");
		else if (e.getActionCommand ().equals ("s3")) 
			cdLayout.show (p_card, "3");

		else if (e.getActionCommand ().equals ("s4"))
			cdLayout.show (p_card, "4");

		else if (e.getActionCommand ().equals ("stand")) {
			for(int i = 0; i< 2; i++)
			{
				thing1();
			}
			
			showStatus("YOU ARE STANDING");
			hit.setEnabled(false);
		}

		else if (e.getActionCommand ().equals ("hit")) {
			showStatus("You gain a card.");
			PlayersCards();
		}


		else if (e.getActionCommand ().equals ("50")) {
			PLbalance -= 50;
			belowBetStop ();
			bet.setText("You Bet: 50");
			balance.setText("Your Balance: "+PLbalance);
			stand.setEnabled(true);
			hit.setEnabled(true);

		}

		else if (e.getActionCommand ().equals ("25")) {
			PLbalance -= 25;
			belowBetStop ();
			bet.setText("You Bet: 25");
			balance.setText("Your Balance: "+PLbalance);
			stand.setEnabled(true);
			hit.setEnabled(true);

		}

		else if (e.getActionCommand ().equals ("10")) {
			PLbalance -= 10;
			bet.setText("You Bet: 10");
			balance.setText("Your Balance: "+PLbalance);
			belowBetStop ();
			stand.setEnabled(true);
			hit.setEnabled(true);
		}

		else if (e.getActionCommand ().equals ("5")) {
			PLbalance -= 5;
			belowBetStop ();
			bet.setText("You Bet: 5");
			balance.setText("Your Balance: "+PLbalance);
			stand.setEnabled(true);
			hit.setEnabled(true);
		}

		else if (e.getActionCommand ().equals ("1")) {
			PLbalance -= 1;
			belowBetStop ();
			bet.setText("You Bet: 1");
			balance.setText("Your Balance: "+PLbalance);
			stand.setEnabled(true);
			hit.setEnabled(true);
			
		}


		else if (e.getActionCommand ().equals ("s5"))
			cdLayout.show (p_card, "5");
		else if (e.getActionCommand ().equals ("s6"))
			System.exit (0);
		else
		{ //code to handle the game
			int n = Integer.parseInt (e.getActionCommand ());
			int x = n / col;
			int y = n % col;
			showStatus ("(" + x + ", " + y + ")");

		}
	}
}
