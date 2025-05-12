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
``` 
# Cow Frequencies 🐄

## 🚀 Description
A C++ simulation that tracks how many cows like each grass patch, labels them as "common" or "unique", identifies the most popular patches, and finds the longest contiguous streak of common grass.  
Built for USACO Bronze prep, but honestly it just turned into a data science project for cows.

## 🧠 What I Learned
- How to use `map` and `vector` to track and analyze frequency data
- How to write structured output and debug logic bugs like a 2000s detective
- What a “common streak” looks like in the wild
- That syntax highlighting in Markdown is a lie unless you close your backticks

## 💻 Tech Stack
C++, STL (map, vector, string), file I/O, raw stubborn willpower

## 🔗 Live Demo / Screenshots
Not live. It’s C++. You compile it.  
But here’s a beautiful output sample:

5 - common
3 - common
5 - common
...
Most liked patch(es): 5 3 2
Longest common streak: 3

bash
Copy
Edit

## 📂 How to Run It
```bash
git clone https://github.com/your-username/cow-frequencies
cd cow-frequencies
g++ -std=c++17 cowfreq.cpp -o cowfreq
./cowfreq
Make sure cowfreq.in exists in the same folder. Output goes to cowfreq.out, because that's how cows roll.
