import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [CommonModule, FormsModule],
  template: `
  <h1>Care Support Website</h1>

  <nav>
    <button (click)="page='home'">Home</button>
    <button (click)="page='contact'">Contact</button>
    <button (click)="page='game'">Game</button>
  </nav>

  <div [ngSwitch]="page">

    <div *ngSwitchCase="'home'">
      <h2>Welcome</h2>
      <p>This website is for Blind, Disabled and Old Age people.</p>
      <button (click)="speak()">🔊 Speak</button>
    </div>

    <div *ngSwitchCase="'contact'">
      <h2>Emergency Contacts</h2>
      <p>Doctor Number: {{doctorNumber}}</p>
      <p>Emergency Number: {{emergencyNumber}}</p>
      <p>Contact Number: {{contactNumber}}</p>
    </div>

    <div *ngSwitchCase="'game'">
      <h2>Guess Game</h2>
      <p>Guess number between 1 to 5</p>
      <input type="number" [(ngModel)]="userGuess">
      <button (click)="check()">Check</button>
      <p>{{message}}</p>
    </div>

  </div>
  `
})
export class AppComponent {

  page = 'home';

  doctorNumber = "9876543210";
  emergencyNumber = "108";
  contactNumber = "9999999999";

  randomNumber = Math.floor(Math.random() * 5) + 1;
  userGuess: number = 0;
  message = "";

  speak() {
    const speech = new SpeechSynthesisUtterance(
      "Welcome to Care Support Website"
    );
    window.speechSynthesis.speak(speech);
  }

  check() {
    if (this.userGuess == this.randomNumber) {
      this.message = "Correct!";
    } else {
      this.message = "Try Again!";
    }
  }
}
