1.  Spring采取以下4种关键策略：

-   基于POJO（Plain Old Java Object——简单的Java对象）的轻量级和最小侵入性编程
-   通过依赖注入和面向接口实现松耦合
-   基于切面和惯例进行声明式编程
-   通过切面和米板减少样板式代码

2.  package com.springinaction.knights;    //松耦合
    > public class BraveKnight implements Knights{
    >     private Quest quest; //Quest是一个所有探险任务都必须实现的接口
    >     //这里BraveKnight没有和任何特定的Quest类型发生耦合，对它来说，被要求挑战的探险任务只要世显了Quest接口，具体是哪一类型的探    险就无关紧要了
    >     public BraveKnight (Quest quest){
    >          this.quest = quest;  //BraveKnight能够响应AQuest、BQuset等任意一种Quest实现
    >     }
    >     public void embarkonQuest throws QuestException{
    >         quest.embark( );
    >     }
    > }

**对依赖进行替换的最常用的方法之一，就是在测试的时候使用mock实现。轻松的测试BraveKnight只需要给它一个Quest的mock实现。**

package com.springinaction.knights;

import static org.mockito.Mockito.\*;
import org.juint.Test;

public class BraveKnightTest{
 @Test
    public void knightShouldEmbarkOnQuest() throw QuestException{
     Quest mockquest = mock(Quest.class); //创建mock的Quest
     BraveKnight knight = new BraveKnight(mockQuest);  //注入mock的Quest
     knight.embarkOnQuest();
    verify(mockQuest,times(1).embark);  //当调用embarkOnQuest()方法时，可以要求Mockito框架验证Quest的mock实现的embark方法仅仅被调用了一次
    }
}

3.  创建应用组件之间的行为通常称为装配。Spring有还能多装配Bean的方式，采用XML配置通常是最常见的装配方式。
      <bean id="knight" class="com.springinaction.knights.BraveKnight">
                      <constructor-arg ref="quest" />      //注入quest Bean
      </bean>
      <bean id="quest"
                    class="com.springinaction.knights.SlayDragonQuest" />     //创建SlayDragonQuest
    </beans>

4.  Spring通过应用上下文（Application Context）装在Bean的定义并把它们组装起来。Spring应用上下文全权负责对象的创建和组装。
