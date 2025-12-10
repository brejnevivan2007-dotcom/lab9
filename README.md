#include <stdio.h>
#include <conio.h>
#include <windows.h>
#include <string.h>

typedef struct {
    int chastota;
    int dlitelnost;
} Note;

void playHappyNewYear() {
    Note melody[] =
    {
        {392, 500}, 
        {392, 500}, 
        {440, 1000},

        {392, 500}, 
        {523, 500}, 
        {494, 1000},

        {392, 500},
        {392, 500},
        {440, 500},
        {392, 500},
        {587, 500},
        {523, 1000},

        {784, 500},
        {659, 500},
        {523, 500}, 
        {494, 500}, 
        {440, 1000},

        {698, 500}, 
        {698, 500}, 
        {659, 500},
        {523, 500},
        {587, 500},
        {523, 1000}
    };

    int notesCount = sizeof(melody) / sizeof(melody[0]);

    printf("\nplay 'Happy New Year'...\n");

    for (int i = 0; i < notesCount; i++) {
        Beep(melody[i].chastota, melody[i].dlitelnost);
        Sleep(0);
    }

    printf("music is end\n");
}
const char* getNoteName(int chastota) {
    switch (chastota) {
    case 262: return "do";
    case 294: return "re";
    case 330: return "mi";
    case 349: return "fa";
    case 392: return "sol'";
    case 440: return "lya";
    case 494: return "si";
    case 523: return "do (up)";
    case 587: return "re (up)";
    case 659: return "mi (up)";
    case 698: return "fa (up)";
    case 784: return "sol' (up)";
    default: return "nota ne naydena";
    }
}

int main() {
    char key;
    printf("console fortepiano\n");
    printf("a-s-d-f-g-h-j: ноты do-re-mi-fa-sol'-lya-si\n");
    printf("p: play 'Happy New Year'\n");
    printf("q: exit\n");
    printf("===========================\n");

    while (1) {
        if (_kbhit()) {
            key = _getch();

            if (key == 'q') {
                printf("\nexit\n");
                break;
            }

            if (key == 'p') {
                playHappyNewYear();
                continue;
            }

            int chastota = 0;
            const char* noteName = "";

            switch (key) {
            case 'a': chastota = 262; break;
            case 's': chastota = 294; break;
            case 'd': chastota = 330; break;
            case 'f': chastota = 349; break;
            case 'g': chastota = 392; break;
            case 'h': chastota = 440; break;
            case 'j': chastota = 494; break;
            default: continue;
            }

            noteName = getNoteName(chastota);
            printf("igrayu notu: %s (s chastotoy: %d Hz)\n", noteName, chastota);

            Beep(chastota, 150);
        }
    }
    return 0;
}
