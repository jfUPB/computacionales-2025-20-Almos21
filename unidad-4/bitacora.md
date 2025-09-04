# Evidencias para la unidad 4

## Código

Código para ofApp.h:

``` cpp
#pragma once
#include "ofMain.h"

// Nodo de la cola
struct Node {
    float x, y;
    float radius;
    ofColor color;
    float opacity;
    Node* next;

    Node(float _x, float _y, float _radius, ofColor _color, float _opacity)
        : x(_x), y(_y), radius(_radius), color(_color), opacity(_opacity), next(nullptr) {
    }
};

// Implementación manual de una cola (FIFO)
class BrushQueue {
public:
    Node* front;
    Node* rear;
    int size;
    int maxSize;

    BrushQueue(int _maxSize);
    ~BrushQueue();

    void enqueue(float x, float y, float radius, ofColor color, float opacity);
    void dequeue();
    void clear();
    bool isEmpty();
};


// Constructor
BrushQueue::BrushQueue(int _maxSize) : front(nullptr), rear(nullptr), size(0), maxSize(_maxSize) {}

// Destructor
BrushQueue::~BrushQueue() {
    clear();
}

// Implementa aquí `enqueue()`
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {
    Node* newNode = new Node(x, y, radius, color, opacity);

    if (isEmpty()) {
        front = rear = newNode;
    }
    else {
        rear->next = newNode;
        rear = newNode;
    }

    size++;
    
    if (size > maxSize) {
        dequeue();
    }
}

// Implementa aquí `dequeue()`
void BrushQueue::dequeue() {
    if (!isEmpty()) {
        Node* temp = front;
        front = front->next;
        delete temp;
        size--;

        if (size == 0) {
            rear = nullptr; // la cola queda vacía
        }
    }
}

// Implementa aquí `clear()`
void BrushQueue::clear() {
    while (!isEmpty()) {
        dequeue();
    }
}

// Implementa aquí `isEmpty()`
bool BrushQueue::isEmpty() {
    return size == 0;
}


class ofApp : public ofBaseApp {
public:
    BrushQueue strokes; // Cola de trazos
    float backgroundHue = 0;

    ofApp() : strokes(50) {} // Tamaño máximo de la cola

    void setup();
    void update();
    void draw();
    void keyPressed(int key);
};
```

Código para ofApp.cpp:

``` cpp
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofBackground(0);
}

//--------------------------------------------------------------
void ofApp::update() {
    backgroundHue += 0.2;
    if (backgroundHue > 255) backgroundHue = 0;

    if (ofGetMousePressed()) {
        float x = ofGetMouseX();
        float y = ofGetMouseY();
        float radius = ofRandom(4.0f, 28.0f);

       
        ofColor color;
        color.setHsb((int)ofRandom(0, 255), 200, 220);

        float opacity = 255.0f;

        strokes.enqueue(x, y, radius, color, opacity);
    }
}

//--------------------------------------------------------------
void ofApp::draw() {
    // Fondo con gradiente dinámico
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    const float minOpacity = 20.0f; 
    int s = strokes.size;
    if (s > 0) {
        Node* node = strokes.front;
        int idx = 0;
        while (node != nullptr) {
            float alpha;
            if (s == 1) {
                alpha = 255.0f;
            }
            else {               
                alpha = ofMap(idx, 0, s - 1, minOpacity, 255.0f, true);
            }
        
            ofColor c = node->color;
            c.a = (unsigned char)ofClamp(alpha, 0.0f, 255.0f);
            ofSetColor(c);
               
            ofDrawCircle(node->x, node->y, node->radius);

            node = node->next;
            idx++;
        }
    }  
    ofSetColor(255);
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'c') {        
        strokes.clear();        
    }
    if (key == 'a') {       
        int newMax = (strokes.maxSize == 50) ? 100 : 50;
        strokes.maxSize = newMax;        
        while (strokes.size > strokes.maxSize) {
            strokes.dequeue();
        }

    }
    else if (key == 's') {
        ofImage screenshot;
        screenshot.grabScreen(0, 0, ofGetWidth(), ofGetHeight());
        std::string filename = "screenshot_" + ofGetTimestampString() + ".png";
        screenshot.save(filename);

    }
}
```

Código para main.cpp:
``` cpp
#include "ofMain.h"
#include "ofApp.h"

//========================================================================
int main() {

	//Use ofGLFWWindowSettings for more options like multi-monitor fullscreen
	ofGLWindowSettings settings;
	settings.setSize(1024, 768);
	settings.windowMode = OF_WINDOW; //can also be OF_FULLSCREEN

	auto window = ofCreateWindow(settings);

	ofRunApp(window, make_shared<ofApp>());
	ofRunMainLoop();

}
```

## Demostración:

[Aquí está el video demostrativo de mi aplicación](https://youtu.be/888I_rrK9E8)

