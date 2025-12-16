#include <stdio.h>
#include <windows.h>
#include <conio.h>

void pianoMode() {
    char key;

    printf("\n==========================================\n");
    printf("          pianino                       ||\n");
    printf("==========================================\n");
    printf("Klavishi:                               ||\n");                          
    printf("  a: do (262 Hz)      s: re (294 Hz)    ||\n");
    printf("  d: mi (330 Hz)      f: fa (349 Hz)    ||\n");
    printf("  g: sol' (392 Hz)    h: lya (440 Hz)   ||\n");
    printf("  j: si (494 Hz)      k: do (523 Hz(up) ||\n");
    printf("------------------------------------------\n");
    printf("  q: vuhod                              ||\n");
    printf("==========================================\n\n");

    while (1) {
        if (_kbhit()) {
            key = _getch();

            if (key == 'q') {
                printf("vuhod\n");
                break;
            }

            int chastota = 0;
            const char* imyanotu = "";

            switch (key) {
            case 'a': chastota = 262; imyanotu = "do"; break;
            case 's': chastota = 294; imyanotu = "re"; break;
            case 'd': chastota = 330; imyanotu = "mi"; break;
            case 'f': chastota = 349; imyanotu = "fa"; break;
            case 'g': chastota = 392; imyanotu = "sol'"; break;
            case 'h': chastota = 440; imyanotu = "lya"; break;
            case 'j': chastota = 494; imyanotu = "si"; break;
            case 'k': chastota = 523; imyanotu = "do (up)"; break;
            default:
                printf("");
                continue;
            }

            printf("play: %s (%d Hz)\n", imyanotu, chastota);
            Beep(chastota, 500);
        }
    }
}
void playProgression() {
    int temp = 750;
    int notu[] = {
        466,
        554,
        698,

        370,
        466,
        554,

        311,
        370,
        466,
    };

    int schetnot = sizeof(notu) / sizeof(notu[0]);

    for (int repeat = 0; repeat < 4; repeat++) {
        printf("povtor %d:\n", repeat + 1);

        for (int i = 0; i < schetnot; i += 3) {
            if (i == 0) printf("  Bbm: ");
            else if (i == 3) printf("  Gb: ");
            else if (i == 6) printf("  Ebm: ");

            Beep(notu[i], temp / 2);
            Beep(notu[i + 1], temp / 2);
            Beep(notu[i + 2], temp);

            printf("✓\n");
            Sleep(100);
        }
        printf("\n");
    }
}
int main() {
    char vubor;
    while (1) {
        printf("\nmain menu:\n");
        printf("  1 - piano\n");
        printf("  2 - music\n");
        printf("  q - exit\n");
        printf("  k - i dont know what is the music\n");

        vubor = getchar();
        while (getchar() != '\n');

        switch (vubor) {
        case '1':
            pianoMode();
            break;

        case '2':
            playProgression();
            break;

        case 'q':
            return 0;

        case 'k':
            printf("Ne znaesh chto za pesnya? eto je: 42 bratyha by 5opka\n");
            break;

        default:
            printf("\n");
        }
    }
    return 0;
}
