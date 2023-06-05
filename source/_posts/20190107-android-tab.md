---
title: '[Android] Tab 구성 시 주의사항'
categories:
  - Programming
  - Mobile
  - Android
tags:
  - Android
  - 안드로이드
  - Tab
date: 2019-01-07 13:42:09
thumbnail: /images/thumbnail/android.png
---

## FragmentStatePagerAdapter의 getItem() 이 두 번 호출될 때

**Viewpager** 를 사용하여 Tab 을 구성하였을 때 **FragmentStatePagerAdapter** 를 사용하였습니다. 탭에 추가한 **Fragment** 와는 상관없이 `getItem()` 이 두 번 호출이 되어서 **Fragment** 를 두 번 로드하게 되는 현상 때문에 문제가 생겨 꼬이게 되었습니다. 이럴경우 **Fragment** 화면이 보일 때와 보이지 않을 때 `setUSerVisiblaHint()` 함수를 사용하여 처리하는데 탭에 추가한 **Fragment** 가 전부 로드되지 않고 어중간하게 두 개의 화면만 로드되었기 때문에 다른 탭을 누르거나 다시 돌아왔을 때 `setUSerVisiblaHint()` 와 `onCreateView()` 함수가 비정상적으로 호출되는 바람에 코딩을 하는데 애먹었습니다.

그래서 찾은 방법은 아래 코드 처럼 **ViewPagerAdapter** 에 **Fragment** 를 3개 추가 하였을 때 `setOffscreenPageLimit()` 함수에 viewPager 에 추가한 Fragement 의 수를 지정하여 화면이 미리 로드되게 하면 `getItem()` 은 Fragement 수 만큼(예: 3번) 호출되지만 앞에서 문제되는 것을 해결할 수 있었습니다.

```java
public class MainActivity extends AppCompatActivity {

    @BindView(R.id.tabs)
    TabLayout tabLayout;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        ButterKnife.bind(this);

        setupViewPager();
    }

    private void setupViewPager() {
        ViewPagerAdapter viewPagerAdapter = new ViewPagerAdapter(getSupportFragmentManager());
        viewPagerAdapter.addFragment(new MobileFragment());
        viewPagerAdapter.addFragment(new LteFragment());
        viewPagerAdapter.addFragment(new WifiFragment());
        viewPager.setOffscreenPageLimit(viewPagerAdapter.getCount());
        viewPager.setAdapter(viewPagerAdapter);
        tabLayout.setupWithViewPager(viewPager);
    }
}
```
