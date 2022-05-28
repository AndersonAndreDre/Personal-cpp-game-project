# myropo


#include <iostream>
#include <iomanip>
#include <cstdlib>
#include <vector>
using namespace std;




class playGame{
    public:





void get_random_position(int &x, int &y, bool alg,vector<vector<char>> board,int SIZE) {
    do {
        x = rand() % SIZE;
        y = rand() % SIZE;
    } while ((!(x >= 0 && x < SIZE) || !(y >= 0 && y < SIZE) || board[x][y] != 0));
    cout << "r"<< x<<"c"<<(char) ('0'+y)<<"  alg" << (alg ? "1" : "2") <<  endl;
}
};
class checkWinner{
    public:


int
count_in_direction(vector<vector<char>> board,int SIZE, int x,  int y, short int m_x, short int m_y) {
    int count = 0;
     char tile = board[x][y];

    while (((x + m_x >= 0) && (x + m_x < SIZE)) && ((y + m_y >= 0) && (y + m_y < SIZE)) &&
           (board[x + m_x][y + m_y] == tile)) {
        x += m_x;
        y += m_y;
        count++;
    }

    return count;
}

bool full_line(vector<vector<char>> board,int SIZE,  int x,  int y) {
    const static int LINE_LENGTH =5;
    const short int directions[4][2] = {{1, 0},
                                        {1, -1},
                                        {0, 1},
                                        {1, 1}};
    for (const auto &direction : directions) {
        if (LINE_LENGTH - 1 <= (count_in_direction(board,SIZE, x, y, direction[0], direction[1]) +
                                count_in_direction(board,SIZE, x, y, -direction[0], -direction[1])))
            return true;
    }

    return false;
}
};
int main() {
    // The variable that for user input or checking the game state.
    int SIZE;
    vector<string> score;
 for(int q=0;q<2;q++){
    cin>>SIZE;
   // vector<vector<int>>matrix(s,vector<int>(s,0));
     vector<vector<char>> board (SIZE,vector<char>(SIZE,0));
    int x, y;
    bool alg = true;
    const static bool alg1 =true;
    const static bool alg2 =true;
  //  ifstream inputFile("input.txt");
//    ofstream outputFile("gomokuResults.txt");


    bool draw;
    checkWinner obj;
    playGame gomoku;

    srand(time(nullptr));

    // Run the game.
    do {
       // gomoku.print_board(board,SIZE);
        if ((alg && alg2) || (!alg && alg1)) {
            gomoku.get_random_position(x, y, alg, board,SIZE);
        } 
        board[x][y] = alg ? 1 : 2;
        if (obj.full_line(board,SIZE, x, y)) {
           score.push_back(alg ? "1" : "2");
           cout<<endl;
            cout <<"win="<< "alg" << (alg ? "1" : "2")<< endl;
            break;
        }

        draw = true;
        for (int k = 0; (k < SIZE) && draw; k++) {
            for (int l = 0; (l < SIZE) && draw; l++) {
                if (board[k][l] == 0) draw = false;
            }
        }

        if (draw) {
           // gomoku.print_board(board,SIZE);
            cout << "Draw game!" << endl;
            break;
        }
        alg = !alg;

    } while (true);

    

 }
 cout<<"wins "<<"Alg"<<score[0]<<" "<<"alg"<<score[1]<<endl;
    
    return 0;
}
