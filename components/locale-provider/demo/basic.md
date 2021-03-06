---
order: 0
title:
  zh-CN: 国际化
  en-US: i18n
---

Wrap your app with `LocaleProvider`, and apply the corresponding language package.

````jsx
import {
  Pagination, LocaleProvider, List, DatePicker, WhiteSpace, InputItem, WingBlank, SegmentedControl,
} from 'antd-mobile';
import enUS from 'antd-mobile/lib/locale-provider/en_US';

const maxDate = new Date(2018, 11, 3, 22, 0);
const minDate = new Date(2015, 7, 6, 8, 30);

const Page = () => (
  <div>
    <Pagination total={5} current={1} />
    <WhiteSpace />
    <List
      className="date-picker-list"
      style={{ backgroundColor: 'white' }}
    >
      <DatePicker
        mode="date"
        title="Select date"
        extra="Click to see i18n text"
        minDate={minDate}
        maxDate={maxDate}
      >
        <List.Item arrow="horizontal">date</List.Item>
      </DatePicker>
    </List>
    <WhiteSpace />
    <InputItem type="money" placeholder="money input" />
  </div>
);

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isEnglish: true,
    };
  }

  onChange = (e) => {
    const index = e.nativeEvent.selectedSegmentIndex;
    this.setState({
      isEnglish: index === 0,
    });
  }

  render() {
    const locale = this.state.isEnglish ? enUS : undefined;
    return (
      <WingBlank>
        <SegmentedControl
          values={['切换到英文', 'change to chinese']}
          selectedIndex={this.state.isEnglish ? 0 : 1}
          onChange={this.onChange}
        />
        <WhiteSpace />
        <LocaleProvider locale={locale}>
          <Page />
        </LocaleProvider>
      </WingBlank>
    );
  }
}

ReactDOM.render(<App />, mountNode);
````
