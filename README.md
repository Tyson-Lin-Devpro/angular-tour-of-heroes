# Angular 課程：英雄之旅

## Angular CLI 指令

- ng new <專案名稱> - 快速創建新ng專案
- ng server --open - 啟動ng應用伺服器
- ng generate component <component名稱> - 創建component並自動導入專案 (簡化指令 ng g c <component名稱>)
- ng generate service <service名稱> :快速建立service (簡化指令 ng g s <service名稱>)


## 1.英雄編輯器

- @Component:
  1.selector:在模板導入的名稱(小寫)，ex. <app-heroes></app-heroes>
  2.templateUrl:使用的模板檔案的位置 ( 寫法 'url路徑.html')
  3.styleUrls:模板獨立的css樣式表位置 ( 寫法 ['url路徑.css'] )

- <input [(ngModel)]="xxx"></input> 
  1.使用於<input>標籤裡雙向綁定(two-way data binding syntax)
  2.不是預設module，須要在app.module.ts中import並加入import:{}裡


## 2.顯示英雄列表

- <xxx *ngFor="let arrayElement of arrayName}"></xxx> :
  1.ng裡遍歷的語法，直接加在標籤裡

- <xxx (event)="functionName(element)"></xxx> :
  1.ng事件綁定寫法
  2.event可以是
    (1)click:點擊事件
    (2)keyup:輸入事件
    (3)keyup.enter:輸入完點擊enter事件
    (4)blur:失去焦點事件

- <xxx *ngIf="變數名"></xxx> :
  1.如果變數有'值'存在則顯示，不存在則不會顯示

- <xxx [class.selected]="hero === selectedHero"></xxx> :
  1.[className]="判別式":判別式成立則將className加入到該元素裡

## 3.建立特性元件

- <componentName [name]="elementName"></componentName> :
  1.將elementName值給予name傳入component
  2.在該component裡引入 (import { Input } from '@angular/core')
  及在class中加入( @Input() name?: Hero; ) 即可順利接收值

## 4.新增服務

- @Injectable({providedIn: 'root'}) :
  1.提供一個可注入的服務
  2.這裡是將服務注入到root裡

- constructor(private heroService: HeroService) {}:
  1.在建構函式新增一個私有的service並宣告型別為HeroService
  2.將HeroService標記為一個注入點

- getHeroes(): void {
  this.heroes = this.heroService.getHeroes();
  } :
  1.建立方法來獲取服務的英雄資料
  2.在ngOnInit() {this.getHeroes()}中調用

- Rxjs :
  1.在component中加入import { Observable, of } from 'rxjs';
  2.將getHeroes()方法改成:
  getHeroes():Observable<Hero[]> {
    const heroes = of(HEROES);
    return heroes;
  }
  3.在需要訂閱的component加入subscribe訂閱(範例是heroes.component.ts中) :
  getHeroes(): void {
  this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes);
  }

## 5.新增導航


