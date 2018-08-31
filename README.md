# Ionic-3-customise-your-enter-loading-and-replace-the-ugly-white-screen-
Tutorial  to solve the ugly white screen issue and to customize your enter loading 


1. create your own logo with respecting the following size and replace the defaut icon under your_app_name/resources/

    icon.png  at least 1024x1024px
    splash.png  at least 2732×2732px
    
2. add mobile platform  to the project.

      ionic cordova platform add ios
      ionic cordova platform add android
      
3.generate your ressources to create icon for all screens types 
      ionic cordova resources
      
      
4.update your config.xml file with the following lines.
   <preference name="AutoHideSplashScreen" value="false" />
    <preference name="FadeSplashScreen" value="true" />
    <preference name="ShowSplashScreen" value="true" />

5.update your  app.component.ts file with the following lines.


         import { timer } from 'rxjs/observable/timer';

      @Component({
        templateUrl: 'app.html'
      })
      export class MyApp {



        showAnimation = true; 

        initializeApp() {
          this.platform.ready().then(() => {

            this.statusBar.styleDefault();
            this.splashScreen.hide();  

            timer(5000).subscribe(() => this.showAnimation = false) // <-- hide animation after 5s
          });
        }

  
6.In the app.html,

    <div *ngIf="showSplash" class="splash">
        <div class="psoload">

          </div>
    </div>
    <ion-nav [root]="rootPage" swipeBackEnabled="false"></ion-nav>


7.app.scss
.splash {
    position: absolute;
    width: 100%;
    height: 100%;
    z-index: 999;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #ff7400;
}

.psoload {
  // your animation code css logic
}


