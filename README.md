# react-native-crash-trigger
A sample native module to integrate react-native application

# Install
```
npm i react-native-crash-trigger

react-native link react-native-crash-trigger
```

# Trigger
When Play button is pressed

# Sample

```
import Player from 'react-native-sample-module';

type Props = {};
export default class App extends Component<Props> {
  constructor(props) {
    super(props);

    this.state = {
      playbackState: 'NONE',
    }

    this.onPlaybackStateChanged = this.onPlaybackStateChanged.bind(this);
  }

  componentDidMount() {
    DeviceEventEmitter.addListener('onPlaybackStateChanged', this.onPlaybackStateChanged);
  }

  componentWillUnmount() {
    DeviceEventEmitter.removeListener('onPlaybackStateChanged', this.onPlaybackStateChanged);
  }

  onPlaybackStateChanged(event) {
    console.log("PlaybackState: " + event.state);
    this.setState({
      playbackState: event.state,
    })
  }

  onPlay() {
    Player.isPlaying((event) => {
      if (!event.playing) {
        Player.play("http://vprbbc.streamguys.net/vprbbc24-mobile.mp3");
      }
    })
  }

  onPause() {
    Player.isPlaying((event) => {
      if (event.playing) {
        Player.pause();
      }
    })
  }

  render() {
    return (
      <View style={styles.container}>
        <View style={{ flexDirection: 'row', alignSelf: 'stretch', justifyContent: 'space-around' }}>
          <Button
            title='Play'
            onPress={() => this.onPlay()}
            color='red'
          />
          <Button
            title='Pause'
            onPress={() => this.onPause()}
            color='red'
          />
        </View>
        <Text style={{ color: 'black', fontSize: 16 }}>{this.state.playbackState}</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});
```


# Original code taken from
https://github.com/kyo504/react-native-sample-module