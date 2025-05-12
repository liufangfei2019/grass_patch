# grass_patch
project counts most liked grass patch
```cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <string>
#include <map>
using namespace std;

struct grass {
    int id;
    string status;
};

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);
    int n;
    ifstream fin("cowfreq.in"); 
    ofstream fout("cowfreq.out"); 
    if (!fin.is_open()) {
        cerr << "file? nonexistent. tragic." << endl;
        return 1;
    }
    fin >> n;
    vector<grass> lawn;

    for (int i = 0; i < n; i++) {
        grass g;
        fin >> g.id;
        g.status = "unknown"; 
        lawn.push_back(g);
    }
    map<int, int> freq;
    for (const auto& g : lawn) {
        freq[g.id]++;
    }
    for (auto& g : lawn) {
    g.status = (freq[g.id] == 1) ? "unique" : "common";
    }
    for (const auto& g : lawn) {
        fout << g.id << " - " << g.status << endl;
    }
    int longest = 0;
    int current = 0;
    
    for (const auto& g : lawn) {
        if (g.status == "common") {
            current++;
            longest = max(longest, current);
        } else {
            current = 0; 
        }
    }
    int maxFreq = 0;
    for (const auto& p : freq) {
        maxFreq = max(maxFreq, p.second); 
    }
    
    vector<int> mostLiked;
    for (const auto& p : freq) {
        if (p.second == maxFreq) {
            mostLiked.push_back(p.first); 
        }
    }
    fout << "Most liked patch(es): ";
    for (int id : mostLiked) {
        fout << id << " ";
    }
    fout << endl;

    fout << "Longest common streak: " << longest << endl;
    return 0;
}
