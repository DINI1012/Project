# Project
Implementasi dan Optimalisasi Sistem Manajemen Playlist Musik pada Platform Spotify

#include <iostream>
#include <string>
using namespace std;

// Struktur untuk lagu
struct Song {
    string judul;
    string penyanyi;
    double durasi;
    Song* next;  // Lagu berikutnya dalam playlist
    // Membuat lagu baru
    Song(string j, string p, double d) {
        judul = j;
        penyanyi = p;
        durasi = d;
        next = NULL;
    }
};
// Struktur untuk playlist
struct Playlist {
    string nama;
    Song* head;  // Lagu pertama dalam playlist
    // Membuat playlist baru
    Playlist(string n) {
        nama = n;
        head = NULL;
    }
    // Menambahkan lagu ke playlist
    void addSong(string judul, string penyanyi, double durasi) {
        Song* newSong = new Song(judul, penyanyi, durasi);
        if (head == NULL) {
            head = newSong;
        } else {
            Song* current = head;
            while (current->next != NULL) {
                current = current->next;
            }
            current->next = newSong;
        }
    }
    // Menampilkan semua lagu dalam playlist
    void displayPlaylist() {
        cout << "Playlist: " << nama << endl;
        cout << "==================" << endl;
        Song* current = head;
        while (current != NULL) {
            cout << "Judul: " << current->judul << endl;
            cout << "Penyanyi: " << current->penyanyi << endl;
            cout << "Durasi: " << current->durasi << " menit" << endl;
            cout << "------------------" << endl;
            current = current->next;
        }
    }
    // Mencari lagu berdasarkan judul
    void searchSong(const string &judul) {
        bool found = false;
        Song* current = head;
        while (current != NULL) {
            if (current->judul == judul) {
                cout << "Judul: " << current->judul << endl;
                cout << "Penyanyi: " << current->penyanyi << endl;
                cout << "Durasi: " << current->durasi << " menit" << endl;
                found = true;
                break;
            }
            current = current->next;
        }
        if (!found) {
            cout << "Lagu dengan judul '" << judul << "' tidak ditemukan dalam playlist '" << nama << "'" << endl;
        }
    }
    // Menghapus semua lagu dalam playlist
    Playlist() {
        Song* current = head;
        while (current != NULL) {
            Song* temp = current;
            current = current->next;
            delete temp;
        }
        head = NULL;
    }
};
int main() {
    // Membuat playlist baru
    Playlist myPlaylist("My Songs");
    // Menambahkan lagu ke playlist
    myPlaylist.addSong("Favorite crime", "Olivia Rodrigo", 2.32);
    myPlaylist.addSong("505", "Arctic Monkeys", 4.13);
    myPlaylist.addSong("Fearless", "Taylor's", 4.01);
    // Menampilkan playlist
    myPlaylist.displayPlaylist();
    // Mencari lagu berdasarkan judul
    myPlaylist.searchSong("505");

    return 0;
}
