조선공학과 2001247 문희윤 

## heeyun01_subscriber

import rclpy
from rclpy.node import Node
from rclpy.qos import QoSProfile
from std_msgs.msg import String

class Heeyun01Subscriber(Node):

    def __init__(self):
        super().__init__('heeyun01_subscriber')
        qos_profile = QoSProfile(depth=10)
        self.subscription = self.create_subscription(
            String,
            'helloworld',
            self.listener_callback,
            qos_profile)
        self.subscription  # prevent unused variable warning

    def listener_callback(self, msg):
        self.get_logger().info('Received message: {0}'.format(msg.data))

def main(args=None):
    rclpy.init(args=args)
    node = Heeyun01Subscriber()
    try:
        rclpy.spin(node)
    except KeyboardInterrupt:
        node.get_logger().info('Keyboard Interrupt (SIGINT)')
    finally:
        node.destroy_node()
        rclpy.shutdown()

if __name__ == '__main__':
    main()

## heeyun01_pubisher

import rclpy
from rclpy.node import Node
from rclpy.qos import QoSProfile
from std_msgs.msg import String

class Heeyun01Publisher(Node):

    def __init__(self):
        super().__init__('heeyun01_publisher')
        qos_profile = QoSProfile(depth=10)
        self.publisher = self.create_publisher(String, 'helloworld', qos_profile)
        self.timer = self.create_timer(1, self.publish_helloworld_msg)
        self.count = 0

    def publish_helloworld_msg(self):
        msg = String()
        msg.data = 'heeyun01: {0}'.format(self.count)
        self.publisher.publish(msg)
        self.get_logger().info('Published message: {0}'.format(msg.data))
        self.count += 1

def main(args=None):
    rclpy.init(args=args)
    node = Heeyun01Publisher()
    try:
        rclpy.spin(node)
    except KeyboardInterrupt:
        node.get_logger().info('Keyboard Interrupt (SIGINT)')
    finally:
        node.destroy_node()
        rclpy.shutdown()

if __name__ == '__main__':
    main()

 ## rqt_graph

 ![스크린샷 2024-05-28 203310](https://github.com/heeyun28/homework1/assets/170499767/831d0e56-a685-418d-ab28-c9443e53b98a)
