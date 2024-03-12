#include <functional>
#include <memory>
#include "rclcpp/rclcpp.hpp"
#include "cpp_topic_pubsub/msg/practice_msg.hpp"


class SubscriberNode : public rclcpp::Node {
public:
    SubscriberNode() : Node("subscriber_node") {  // rclcpp::Nodeを継承してsubscriber_nodeというNodeを作成
        auto topic_callback = [this](const cpp_topic_pubsub::msg::PracticeMsg &msg) -> void {
            RCLCPP_INFO(this->get_logger(), "product name: %s, price: %d", msg.name.c_str(), msg.price);
        };  // topicにメッセージが送られてきた時に呼び出されるcallback

        subscription_ = this->create_subscription<cpp_topic_pubsub::msg::PracticeMsg>
                ("practice_topic", 10, topic_callback);  // topicをsubscribeする為の設定
    }
private:
    // 上記の動作に必要なprivateメンバ
    rclcpp::Subscription<cpp_topic_pubsub::msg::PracticeMsg>::SharedPtr subscription_;
};

int main(int argc, char *argv[]) {
    rclcpp::init(argc, argv);
    rclcpp::spin(std::make_shared<SubscriberNode>());
    rclcpp::shutdown();
    return 0;
}