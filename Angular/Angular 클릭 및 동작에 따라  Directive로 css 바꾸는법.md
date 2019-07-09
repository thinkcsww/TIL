​								Angular 클릭 및 동작에 따라  Directive로 css 바꾸는법

------

1. ng c d [이름]으로 Directive를 생성한다.
2. @HostBinding()으로 바꾸고 싶은 attribute를 생성한다.
3. @HostListener()에서 attribute를 변경한다. 

예시 

```
import {Directive, HostBinding, HostListener} from "@angular/core";

@Directive({
  selector: '[appDropdown]'
})
export class DropdownDirective {
  @HostBinding('class.open') isOpen = false;

  // 이 함수 이름은 맘대로 해도된다.
  @HostListener('click') toggleOpen() {
    this.isOpen = !this.isOpen;
  }
}

```

