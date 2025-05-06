---
title: "Abstract Factory Pattern"
---

# Abstract Factory Example in Game Engine Design

### Overview
This page demonstrates the use of the **Abstract Factory** design pattern in the context of game engine development. The pattern is used to create families of related or dependent objects without specifying their concrete classes. This is particularly useful in game engines when supporting multiple rendering backends, input systems, or UI toolkits that must be interchangeable without modifying core engine logic.

---

### Use Case: Cross-Platform UI Rendering
Suppose we are designing a game engine that needs to support multiple UI systems, such as one for PC and another for mobile platforms. Each platform will have its own style of buttons and windows. The Abstract Factory pattern allows the engine to create UI elements specific to the target platform without altering the game logic.

---

### Abstract Factory Interface

```cpp
class GUIFactory {
public:
    virtual Button* createButton() = 0;
    virtual Window* createWindow() = 0;
    virtual ~GUIFactory() {}
};
```

### Concrete Factories

```cpp
class PCGUIFactory : public GUIFactory {
public:
    Button* createButton() override {
        return new PCButton();
    }
    Window* createWindow() override {
        return new PCWindow();
    }
};

class MobileGUIFactory : public GUIFactory {
public:
    Button* createButton() override {
        return new MobileButton();
    }
    Window* createWindow() override {
        return new MobileWindow();
    }
};
```

### Abstract Product Interfaces

```cpp
class PCButton : public Button {
public:
    void render() override {
        std::cout << "Rendering PC-style button" << std::endl;
    }
};

class MobileButton : public Button {
public:
    void render() override {
        std::cout << "Rendering Mobile-style button" << std::endl;
    }
};

class PCWindow : public Window {
public:
    void open() override {
        std::cout << "Opening PC-style window" << std::endl;
    }
};

class MobileWindow : public Window {
public:
    void open() override {
        std::cout << "Opening Mobile-style window" << std::endl;
    }
};
```

### Client Code

```cpp
void initializeUI(GUIFactory* factory) {
    Button* button = factory->createButton();
    Window* window = factory->createWindow();

    button->render();
    window->open();

    delete button;
    delete window;
}
```

### Conclusion

The Abstract Factory pattern enables modular and scalable architecture in game engines. By abstracting the creation of platform-specific components, we maintain clean separation of concerns and facilitate platform switching or extension with minimal code changes. This is especially valuable in cross-platform engine development workflows.