# StackCardsView

�ѵ������ؼ����������罻���̽̽��Ч����������������չ��

- **֧�ֻ����������**
- **֧����ʧ�������**
- **����Ƕ��ViewPager�Ȼ����ؼ�**
- **֧����ǶListView,RecycleView�Ȼ����ؼ�**


-------------------

Ч����ʾ
-------

 ![��ʾ1-���ٻ����ɳ�](demo-images/demo1.gif)&ensp;&ensp;&ensp;&ensp;&ensp;![��ʾ2-������Ʒɳ�](demo-images/demo2.gif)
<br/><br/>
![��ʾ3-Ƕ�뵽ViewPager](demo-images/demo3.gif)&ensp;&ensp;&ensp;&ensp;&ensp;![��ʾ4-��ǶRecycleView](demo-images/demo4.gif)

-------------------

���ʹ��
-------

 - xml����StackCardsView:

``` xml
    <com.beyondsw.lib.widget.StackCardsView
        android:id="@+id/cards"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:itemHeight="340dp"
        app:itemWidth="340dp"
        android:paddingBottom="66dp"
        android:clipToPadding="false"
        />
```
֧�ֵ�xml�������ã�
| ������      |    ˵�� | ����  |�Ƿ����|
| :-------- | :------| :-- |:--: |
| itemWidth  | ��Ƭ��� |  dimension   |��|
| itemHeight     |   ��Ƭ�߶� |  dimension  |��|
| maxVisibleCnt      |    ������ʱ�����Կ����Ŀ�Ƭ�� | integer  |��|
| edgeHeight      |    ���Ч���߶� | dimension  |��|
| scaleFactor      |    ÿ��������ϲ��scaleϵ�� | float  |��|
| alphaFactor      |    ÿ��������ϲ��alphaϵ�� | float  |��|
| dismissFactor      |    �������볬���ؼ���ȵĶ��ٱ���ʱ��ʧ | float  |��|
| dismissAlpha      |   //todo,��Ƭ��ʧʱ��͸���ȣ���δʵ�� | float  |��|
| dragSensitivity      |    ���������� | float  |��|
<br/><br/>
 - xml����StackCardsView:
 
 

``` java
����adapter:

  mCardsView = Utils.findViewById(root,R.id.cards);
  mCardsView.addOnCardSwipedListener(this);
  mAdapter = new CardAdapter();
  mCardsView.setAdapter(mAdapter);


public class CardAdapter extends StackCardsView.Adapter {

    private List<BaseCardItem> mItems;

    public void appendItems(List<BaseCardItem> items){
        int size = items == null ? 0 : items.size();
        if (size == 0) {
            return;
        }
        if (mItems == null) {
            mItems = new ArrayList<>(size);
        }
        mItems.addAll(items);
        notifyDataSetChanged();
    }

    public void remove(int position){
        mItems.remove(position);
        notifyItemRemoved(position);
    }

    @Override
    public int getCount() {
        return mItems == null ? 0 : mItems.size();
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        return mItems.get(position).getView(convertView,parent);
    }

    @Override
    public int getSwipeDirection(int position) {
        //�������ÿ�ſ���֧�ֻ�������һ��������ʧ�ķ���
        BaseCardItem item = mItems.get(position);
        return item.swipeDir;
    }

    @Override
    public int getDismissDirection(int position) {
        //�������ÿ�ſ���֧�ֻ�������һ��������ʧ�ķ���
        BaseCardItem item = mItems.get(position);
        return item.dismissDir;
    }

    @Override
    public boolean isFastDismissAllowed(int position) {
        //�������ÿ�ſ���֧�ֿ��ٻ�����ʧ�ķ���
        BaseCardItem item = mItems.get(position);
        return item.fastDismissAllowed;
    }

    @Override
    public int getMaxRotation(int position) {
         //�������ÿ�ſ��������ת��
        BaseCardItem item = mItems.get(position);
        return item.maxRotation;
    }
}
```


[���ⷴ��](https://github.com/wensefu/StackCardsView/issues "���ⷴ��")


License
-------

    Copyright 2017 wensefu
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.