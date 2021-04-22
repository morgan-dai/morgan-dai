//Tic tac toe game program
#include <vector>
#include <iostream>

using namespace std;

const int PLAYER1 = 0;              //Global variables
const int PLAYER2 = 1;
int turn = PLAYER1;


void duringGame()                   //Informs players of whos' turn it is
{
    cout << endl;
   
    if (turn == PLAYER1) {
        cout << "Enter a letter for placement (X's turn): " << endl;
    }
    else {
        cout << "Enter a letter for placement (O's turn): " << endl;
    }
}

void drawBoard(const vector <char> &tttBoard)       //Placement of game board
{

duringGame();

for (int i = 0; i < 9; i += 3)
{
cout << "  " << tttBoard.at(i) << "  |  " << tttBoard.at(i + 1) << "  |  ";
cout << tttBoard.at(i + 2) << "  " << endl;
if (i < 6)
cout << "-----|-----|-----" << endl;
}
cout << endl;
}

void initVector(vector <char> &y)               //letter within game board to determine placement
{
if (y.size() <= 26)
{
for (int i = 0; i < y.size(); ++i)
{
y.at(i) = 'a' + i;
}
}

return;
}

int newPlacement(char position)                 //Locates the position
{
vector <char> v1(9);

initVector(v1);

for (int i = 0; i < v1.size(); ++i)
{
if (position == v1.at(i))
return i;
}

return 10;
}

bool userChoice(const vector <char> &tttBoard, int position)                //Determines position availability
{
if (position < tttBoard.size())
{
if ((tttBoard.at(position) != 'X' && tttBoard.at(position) != 'O'))
return true;
}
else
return false;
}

int getPlay(const vector <char> &tttBoard)                      //Player input
{
char position;
int index;

do
{
cin >> position;
cout << endl;

index = newPlacement(position);
} while ((!userChoice(tttBoard, index)));
return index;
}

bool winner(const vector <char> &tttBoard)                      //Checks for a win condition
{
for (int i = 0; i < 3; ++i)
{
if (tttBoard.at(3 * i) == tttBoard.at(3 * i + 1)
&& tttBoard.at(3 * i + 1) == tttBoard.at(3 * i + 2))
return true;
else if (tttBoard.at(i) == tttBoard.at(i + 3) && tttBoard.at(i + 3) == tttBoard.at(i + 6))
return true;
}

if (tttBoard.at(0) == tttBoard.at(4) && tttBoard.at(4) == tttBoard.at(8))
return true;
else if (tttBoard.at(2) == tttBoard.at(4) && tttBoard.at(4) == tttBoard.at(6))
return true;

return false;
}

bool boardFull(const vector <char> &tttBoard)                   //Determines if the board is full
{

int j = 0;
for (int i = 0; i < tttBoard.size(); ++i)
{
if (tttBoard.at(i) == 'X' || tttBoard.at(i) == 'O')
j++;
}

if (j == 9)
return true;
else
return false;
}


int main()                                              //Progresses the game
{
vector <char> tttBoard(9);
int play;

initVector(tttBoard);
drawBoard(tttBoard);

       while (!boardFull(tttBoard) && !winner(tttBoard))
{
play = getPlay(tttBoard);

tttBoard.at(play) = (turn == PLAYER1) ? 'X' : 'O';


if (!boardFull(tttBoard) && !winner(tttBoard))
{
if (turn == PLAYER1)
turn = PLAYER2;
else if (turn == PLAYER2)
turn = PLAYER1;
}

drawBoard(tttBoard);
}
if (turn == PLAYER1 && winner(tttBoard))
cout << "X wins!" << endl << endl;
else if (turn == PLAYER2 && winner(tttBoard))
cout << "O wins!" << endl << endl;
else
cout << "It is a draw." << endl << endl;


return 0;
}

